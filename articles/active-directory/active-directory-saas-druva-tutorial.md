---
title: "Tutorial: integração do Azure Active Directory com Druva | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Druva."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: ab92b600-1fea-4905-b1c7-ef8e4d8c495c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: b23e73c47b9a00893e036b67826e4b7ead819a1d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-druva"></a><span data-ttu-id="24c12-103">Tutorial: integração do Azure Active Directory com o Druva</span><span class="sxs-lookup"><span data-stu-id="24c12-103">Tutorial: Azure Active Directory integration with Druva</span></span>

<span data-ttu-id="24c12-104">Neste tutorial, você aprenderá a integrar o Druva ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="24c12-104">In this tutorial, you learn how to integrate Druva with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="24c12-105">A integração do Druva ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="24c12-105">Integrating Druva with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="24c12-106">No Azure AD, é possível controlar quem tem acesso ao Druva.</span><span class="sxs-lookup"><span data-stu-id="24c12-106">You can control in Azure AD who has access to Druva.</span></span>
- <span data-ttu-id="24c12-107">Você pode permitir que os usuários entrem automaticamente no Druva (Logon Único) com as respectivas contas do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="24c12-107">You can enable your users to automatically get signed-on to Druva (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="24c12-108">Você pode gerenciar suas contas em um único local central – o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="24c12-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="24c12-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="24c12-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="24c12-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="24c12-110">Prerequisites</span></span>

<span data-ttu-id="24c12-111">Para configurar a integração do Azure AD ao Druva, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="24c12-111">To configure Azure AD integration with Druva, you need the following items:</span></span>

- <span data-ttu-id="24c12-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="24c12-112">An Azure AD subscription</span></span>
- <span data-ttu-id="24c12-113">Uma assinatura habilitada para logon único do Druva</span><span class="sxs-lookup"><span data-stu-id="24c12-113">A Druva single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="24c12-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="24c12-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="24c12-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="24c12-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="24c12-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="24c12-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="24c12-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="24c12-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="24c12-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="24c12-118">Scenario description</span></span>
<span data-ttu-id="24c12-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="24c12-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="24c12-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="24c12-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="24c12-121">Adicionar o Druva da galeria</span><span class="sxs-lookup"><span data-stu-id="24c12-121">Adding Druva from the gallery</span></span>
2. <span data-ttu-id="24c12-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="24c12-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-druva-from-the-gallery"></a><span data-ttu-id="24c12-123">Adicionar o Druva da galeria</span><span class="sxs-lookup"><span data-stu-id="24c12-123">Adding Druva from the gallery</span></span>
<span data-ttu-id="24c12-124">Para configurar a integração do Druva com o Azure AD, você precisará adicionar o Druva da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="24c12-124">To configure the integration of Druva into Azure AD, you need to add Druva from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="24c12-125">**Para adicionar o Druva da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="24c12-125">**To add Druva from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="24c12-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="24c12-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![O botão Azure Active Directory][1]

2. <span data-ttu-id="24c12-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="24c12-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="24c12-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="24c12-129">Then go to **All applications**.</span></span>

    ![A folha Aplicativos empresariais][2]
    
3. <span data-ttu-id="24c12-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="24c12-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![O botão Novo aplicativo][3]

4. <span data-ttu-id="24c12-133">Na caixa de pesquisa, digite **Druva**, selecione **Druva** no painel de resultados e, depois, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="24c12-133">In the search box, type **Druva**, select **Druva** from result panel then click **Add** button to add the application.</span></span>

    ![Druva na lista de resultados](./media/active-directory-saas-druva-tutorial/tutorial_druva_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="24c12-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="24c12-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="24c12-136">Nesta seção, você configurará e testará o logon único do Azure AD com o Druva, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="24c12-136">In this section, you configure and test Azure AD single sign-on with Druva based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="24c12-137">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Druva é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="24c12-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Druva is to a user in Azure AD.</span></span> <span data-ttu-id="24c12-138">Em outras palavras, é necessário estabelecer uma relação de vinculação entre um usuário do Azure AD e o usuário relacionado do Druva.</span><span class="sxs-lookup"><span data-stu-id="24c12-138">In other words, a link relationship between an Azure AD user and the related user in Druva needs to be established.</span></span>

<span data-ttu-id="24c12-139">No Druva, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="24c12-139">In Druva, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="24c12-140">Para configurar e testar o logon único do Azure AD com o Druva, você precisará concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="24c12-140">To configure and test Azure AD single sign-on with Druva, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="24c12-141">**[Configurar o logon único do Azure AD](#configure-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="24c12-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="24c12-142">**[Criar um usuário de teste do Azure AD](#create-an-azure-ad-test-user)** – para testar o logon único do Azure AD com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="24c12-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="24c12-143">**[Criar um usuário de teste do Druva](#create-a-druva-test-user)** – para ter um equivalente de Brenda Fernandes no Druva vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="24c12-143">**[Create a Druva test user](#create-a-druva-test-user)** - to have a counterpart of Britta Simon in Druva that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="24c12-144">**[Atribuir o usuário de teste do Azure AD](#assign-the-azure-ad-test-user)** – para permitir que Brenda Fernandes use o logon único do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="24c12-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="24c12-145">**[Teste o logon único](#test-single-sign-on)** – para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="24c12-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="24c12-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="24c12-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="24c12-147">Nesta seção, você habilitará o logon único do Azure AD no Portal do Azure e configurará o logon único no aplicativo Druva.</span><span class="sxs-lookup"><span data-stu-id="24c12-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Druva application.</span></span>

<span data-ttu-id="24c12-148">**Para configurar o logon único do Azure AD com o Druva, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="24c12-148">**To configure Azure AD single sign-on with Druva, perform the following steps:**</span></span>

1. <span data-ttu-id="24c12-149">No Portal do Azure, na página de integração de aplicativos do **Druva**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="24c12-149">In the Azure portal, on the **Druva** application integration page, click **Single sign-on**.</span></span>

    ![Link Configurar logon único][4]

2. <span data-ttu-id="24c12-151">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="24c12-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-druva-tutorial/tutorial_druva_samlbase.png)

3. <span data-ttu-id="24c12-153">Na seção **Domínio e URLs do Druva**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="24c12-153">On the **Druva Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-druva-tutorial/tutorial_druva_url.png)

    <span data-ttu-id="24c12-155">Na caixa de texto **URL de Logon**, digite a URL: `https://cloud.druva.com/home`</span><span class="sxs-lookup"><span data-stu-id="24c12-155">In the **Sign-on URL** textbox, type the URL: `https://cloud.druva.com/home`</span></span>

4. <span data-ttu-id="24c12-156">Na seção **Certificado de Autenticação do SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado no computador.</span><span class="sxs-lookup"><span data-stu-id="24c12-156">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![O link de download do Certificado](./media/active-directory-saas-druva-tutorial/tutorial_druva_certificate.png) 

5. <span data-ttu-id="24c12-158">Seu aplicativo Druva espera as declarações do SAML em um formato específico, o que exige que você adicione mapeamentos de atributo personalizados de acordo com a sua configuração de **Atributos do Token SAML**.</span><span class="sxs-lookup"><span data-stu-id="24c12-158">Your Druva application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your **SAML Token Attributes** configuration.</span></span> 

    ![Configurar Logon Único](./media/active-directory-saas-druva-tutorial/tutorial_druva_attribute.png)

6. <span data-ttu-id="24c12-160">Na seção **Atributos de Usuário** da caixa de diálogo **Logon único**, configure o atributo do token SAML, conforme mostrado na imagem anterior e realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="24c12-160">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the preceding image and perform the following steps:</span></span>

    | <span data-ttu-id="24c12-161">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="24c12-161">Attribute Name</span></span>      | <span data-ttu-id="24c12-162">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="24c12-162">Attribute Value</span></span>      |
    | ------------------- | -------------------- |
    | <span data-ttu-id="24c12-163">insync\_auth\_token</span><span class="sxs-lookup"><span data-stu-id="24c12-163">insync\_auth\_token</span></span> |<span data-ttu-id="24c12-164">Insira o valor gerado pelo token</span><span class="sxs-lookup"><span data-stu-id="24c12-164">Enter the token generated value</span></span> |
    
    <span data-ttu-id="24c12-165">a.</span><span class="sxs-lookup"><span data-stu-id="24c12-165">a.</span></span> <span data-ttu-id="24c12-166">Clique em **Adicionar atributo** para abrir o diálogo **Adicionar Atributo**.</span><span class="sxs-lookup"><span data-stu-id="24c12-166">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>
    
    ![Configurar o logon único](./media/active-directory-saas-druva-tutorial/tutorial_attribute_04.png)
    
    ![Configurar Logon Único](./media/active-directory-saas-druva-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="24c12-169">b.</span><span class="sxs-lookup"><span data-stu-id="24c12-169">b.</span></span> <span data-ttu-id="24c12-170">Na caixa de texto **Nome** , digite o nome do atributo mostrado para essa linha.</span><span class="sxs-lookup"><span data-stu-id="24c12-170">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="24c12-171">c.</span><span class="sxs-lookup"><span data-stu-id="24c12-171">c.</span></span> <span data-ttu-id="24c12-172">Na lista **Valor**, digite o valor do atributo mostrado para essa linha.</span><span class="sxs-lookup"><span data-stu-id="24c12-172">From the **Value** list, type the attribute value shown for that row.</span></span> <span data-ttu-id="24c12-173">O valor gerado pelo token é explicado posteriormente no tutorial.</span><span class="sxs-lookup"><span data-stu-id="24c12-173">The token generated value is explained later in tutorial.</span></span>
    
    <span data-ttu-id="24c12-174">d.</span><span class="sxs-lookup"><span data-stu-id="24c12-174">d.</span></span> <span data-ttu-id="24c12-175">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="24c12-175">Click **Ok**.</span></span>    

7. <span data-ttu-id="24c12-176">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="24c12-176">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-druva-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="24c12-178">Na seção **Configuração do Druva**, clique em **Configurar o Druva** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="24c12-178">On the **Druva Configuration** section, click **Configure Druva** to open **Configure sign-on** window.</span></span> <span data-ttu-id="24c12-179">Copie a **URL do serviço de logon único do SAML e a URL de logoff** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="24c12-179">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-druva-tutorial/tutorial_druva_configure.png) 

9. <span data-ttu-id="24c12-181">Em outra janela do navegador da Web, faça logon em seu site de empresa do Druva como administrador.</span><span class="sxs-lookup"><span data-stu-id="24c12-181">In a different web browser window, log in to your Druva company site as an administrator.</span></span>

10. <span data-ttu-id="24c12-182">Vá para **Gerenciar \> Configurações**.</span><span class="sxs-lookup"><span data-stu-id="24c12-182">Go to **Manage \> Settings**.</span></span>

    <span data-ttu-id="24c12-183">![Configurações](./media/active-directory-saas-druva-tutorial/ic795091.png "Configurações")</span><span class="sxs-lookup"><span data-stu-id="24c12-183">![Settings](./media/active-directory-saas-druva-tutorial/ic795091.png "Settings")</span></span>

11. <span data-ttu-id="24c12-184">Na caixa de diálogo Configurações de Logon Único, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="24c12-184">On the Single Sign-On Settings dialog, perform the following steps:</span></span>

    <span data-ttu-id="24c12-185">![Configurações de Logon Único](./media/active-directory-saas-druva-tutorial/ic795092.png "Configurações de Logon Único")</span><span class="sxs-lookup"><span data-stu-id="24c12-185">![Single Sign-On Settings](./media/active-directory-saas-druva-tutorial/ic795092.png "Single Sign-On Settings")</span></span>
    
    <span data-ttu-id="24c12-186">a.</span><span class="sxs-lookup"><span data-stu-id="24c12-186">a.</span></span> <span data-ttu-id="24c12-187">Cole o valor da **URL do Serviço de Logon Único SAML** copiado do Portal do Azure na caixa de texto **URL de Logon do Provedor de ID**.</span><span class="sxs-lookup"><span data-stu-id="24c12-187">Paste **SAML Single Sign-On Service URL** value, which you have copied from the Azure portal into the **ID Provider Login URL** textbox.</span></span>
    
    <span data-ttu-id="24c12-188">b.</span><span class="sxs-lookup"><span data-stu-id="24c12-188">b.</span></span> <span data-ttu-id="24c12-189">Cole o valor da **URL de Saída** copiado do Portal do Azure na caixa de texto **URL de Logon do Provedor de ID**.</span><span class="sxs-lookup"><span data-stu-id="24c12-189">Paste **Sign-Out URL** value, which you have copied from the Azure portal into the **ID Provider Logout URL** textbox.</span></span>
    
     <span data-ttu-id="24c12-190">c.</span><span class="sxs-lookup"><span data-stu-id="24c12-190">c.</span></span> <span data-ttu-id="24c12-191">Abra seu certificado codificado em Base 64 no bloco de notas, copie o conteúdo dele na área de transferência e cole-o na caixa de texto **Certificado do Provedor de ID**</span><span class="sxs-lookup"><span data-stu-id="24c12-191">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **ID Provider Certificate** textbox</span></span>
     
     <span data-ttu-id="24c12-192">d.</span><span class="sxs-lookup"><span data-stu-id="24c12-192">d.</span></span> <span data-ttu-id="24c12-193">Para abrir a página **Configurações**, clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="24c12-193">To open the **Settings** page, click **Save**.</span></span>

12. <span data-ttu-id="24c12-194">Na página **Configurações**, clique em **Gerar Token de SSO**.</span><span class="sxs-lookup"><span data-stu-id="24c12-194">On the **Settings** page, click **Generate SSO Token**.</span></span>

    <span data-ttu-id="24c12-195">![Configurações](./media/active-directory-saas-druva-tutorial/ic795093.png "Configurações")</span><span class="sxs-lookup"><span data-stu-id="24c12-195">![Settings](./media/active-directory-saas-druva-tutorial/ic795093.png "Settings")</span></span>

13. <span data-ttu-id="24c12-196">No diálogo **Token de Autenticação de Logon Único** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="24c12-196">On the **Single Sign-on Authentication Token** dialog, perform the following steps:</span></span>

    <span data-ttu-id="24c12-197">![Token SSO](./media/active-directory-saas-druva-tutorial/ic795094.png "Token SSO")</span><span class="sxs-lookup"><span data-stu-id="24c12-197">![SSO Token](./media/active-directory-saas-druva-tutorial/ic795094.png "SSO Token")</span></span>
    
    <span data-ttu-id="24c12-198">a.</span><span class="sxs-lookup"><span data-stu-id="24c12-198">a.</span></span> <span data-ttu-id="24c12-199">Clique em **Copiar**, cole o valor copiado na caixa de texto **Valor** na seção **Adicionar Atributo**.</span><span class="sxs-lookup"><span data-stu-id="24c12-199">Click **Copy**, Paste copied value in the **Value** textbox in the **Add Attribute** section.</span></span>
    
    <span data-ttu-id="24c12-200">b.</span><span class="sxs-lookup"><span data-stu-id="24c12-200">b.</span></span> <span data-ttu-id="24c12-201">Clique em **fechar**</span><span class="sxs-lookup"><span data-stu-id="24c12-201">Click **Close**.</span></span>

> [!TIP]
> <span data-ttu-id="24c12-202">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="24c12-202">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="24c12-203">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="24c12-203">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="24c12-204">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="24c12-204">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="24c12-205">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="24c12-205">Create an Azure AD test user</span></span>

<span data-ttu-id="24c12-206">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="24c12-206">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Criar um usuário de teste do Azure AD][100]

<span data-ttu-id="24c12-208">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="24c12-208">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="24c12-209">No portal do Azure, no painel esquerdo, clique no botão **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="24c12-209">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![O botão Azure Active Directory](./media/active-directory-saas-druva-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="24c12-211">Para exibir a lista de usuários, acesse **Usuários e grupos** e, depois, clique em **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="24c12-211">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Os links “Usuários e grupos” e “Todos os usuários”](./media/active-directory-saas-druva-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="24c12-213">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo **Todos os Usuários**.</span><span class="sxs-lookup"><span data-stu-id="24c12-213">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![O botão Adicionar](./media/active-directory-saas-druva-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="24c12-215">Na caixa de diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="24c12-215">In the **User** dialog box, perform the following steps:</span></span>

    ![A caixa de diálogo Usuário](./media/active-directory-saas-druva-tutorial/create_aaduser_04.png)

    <span data-ttu-id="24c12-217">a.</span><span class="sxs-lookup"><span data-stu-id="24c12-217">a.</span></span> <span data-ttu-id="24c12-218">Na caixa **Nome**, digite **BrendaFernandes**.</span><span class="sxs-lookup"><span data-stu-id="24c12-218">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="24c12-219">b.</span><span class="sxs-lookup"><span data-stu-id="24c12-219">b.</span></span> <span data-ttu-id="24c12-220">Na caixa **Nome de usuário**, digite o endereço de email do usuário Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="24c12-220">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="24c12-221">c.</span><span class="sxs-lookup"><span data-stu-id="24c12-221">c.</span></span> <span data-ttu-id="24c12-222">Marque a caixa de seleção **Mostrar Senha** e, em seguida, anote o valor exibido na caixa **Senha**.</span><span class="sxs-lookup"><span data-stu-id="24c12-222">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="24c12-223">d.</span><span class="sxs-lookup"><span data-stu-id="24c12-223">d.</span></span> <span data-ttu-id="24c12-224">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="24c12-224">Click **Create**.</span></span>
 
### <a name="create-a-druva-test-user"></a><span data-ttu-id="24c12-225">Criar um usuário de teste do Druva</span><span class="sxs-lookup"><span data-stu-id="24c12-225">Create a Druva test user</span></span>

<span data-ttu-id="24c12-226">Para permitir que os usuários do Azure AD façam logon no Druva, eles devem estar provisionados no Druva.</span><span class="sxs-lookup"><span data-stu-id="24c12-226">In order to enable Azure AD users to log in to Druva, they must be provisioned into Druva.</span></span> <span data-ttu-id="24c12-227">No caso do Druva, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="24c12-227">In the case of Druva, provisioning is a manual task.</span></span>

<span data-ttu-id="24c12-228">**Para configurar o provisionamento de usuários, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="24c12-228">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="24c12-229">Faça logon em seu site de empresa do **Druva** como administrador.</span><span class="sxs-lookup"><span data-stu-id="24c12-229">Log in to your **Druva** company site as administrator.</span></span>

2. <span data-ttu-id="24c12-230">Vá para **Gerenciar \> Usuários**.</span><span class="sxs-lookup"><span data-stu-id="24c12-230">Go to **Manage \> Users**.</span></span>
   
   <span data-ttu-id="24c12-231">![Gerenciar Usuários](./media/active-directory-saas-druva-tutorial/ic795097.png "Gerenciar Usuários")</span><span class="sxs-lookup"><span data-stu-id="24c12-231">![Manage Users](./media/active-directory-saas-druva-tutorial/ic795097.png "Manage Users")</span></span>

3. <span data-ttu-id="24c12-232">Clique em **Criar Novo**.</span><span class="sxs-lookup"><span data-stu-id="24c12-232">Click **Create New**.</span></span>
   
   <span data-ttu-id="24c12-233">![Gerenciar Usuários](./media/active-directory-saas-druva-tutorial/ic795098.png "Gerenciar Usuários")</span><span class="sxs-lookup"><span data-stu-id="24c12-233">![Manage Users](./media/active-directory-saas-druva-tutorial/ic795098.png "Manage Users")</span></span>

4. <span data-ttu-id="24c12-234">Na caixa de diálogo Criar Novo Usuário, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="24c12-234">On the Create New User dialog, perform the following steps:</span></span>
   
   <span data-ttu-id="24c12-235">![Criar Novo Usuário](./media/active-directory-saas-druva-tutorial/ic795099.png "Criar Novo Usuário")</span><span class="sxs-lookup"><span data-stu-id="24c12-235">![Create NewUser](./media/active-directory-saas-druva-tutorial/ic795099.png "Create NewUser")</span></span>
   
   <span data-ttu-id="24c12-236">a.</span><span class="sxs-lookup"><span data-stu-id="24c12-236">a.</span></span> <span data-ttu-id="24c12-237">Na caixa de texto **Endereço de email**, insira o email do usuário como **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="24c12-237">In the **Email address** textbox, enter the email of user like **brittasimon@contoso.com**.</span></span>
   
   <span data-ttu-id="24c12-238">b.</span><span class="sxs-lookup"><span data-stu-id="24c12-238">b.</span></span> <span data-ttu-id="24c12-239">Na caixa de texto **Nome**, insira o nome de usuário, como **BrendaFernandes**.</span><span class="sxs-lookup"><span data-stu-id="24c12-239">In the **Name** textbox, enter the name of user like **BrittaSimon**.</span></span>
   
   <span data-ttu-id="24c12-240">c.</span><span class="sxs-lookup"><span data-stu-id="24c12-240">c.</span></span> <span data-ttu-id="24c12-241">Clique em **Criar Usuário**.</span><span class="sxs-lookup"><span data-stu-id="24c12-241">Click **Create User**.</span></span>

>[!NOTE]
><span data-ttu-id="24c12-242">É possível usar qualquer outra ferramenta de criação da conta de usuário do Druva ou as APIs fornecidas pelo Druva para provisionar as contas de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="24c12-242">You can use any other Druva user account creation tools or APIs provided by Druva to provision Azure AD user accounts.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="24c12-243">Atribuir o usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="24c12-243">Assign the Azure AD test user</span></span>

<span data-ttu-id="24c12-244">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao Druva.</span><span class="sxs-lookup"><span data-stu-id="24c12-244">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Druva.</span></span>

![Atribuir a função de usuário][200] 

<span data-ttu-id="24c12-246">**Para atribuir Brenda Fernandes ao Druva, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="24c12-246">**To assign Britta Simon to Druva, perform the following steps:**</span></span>

1. <span data-ttu-id="24c12-247">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="24c12-247">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="24c12-249">Na lista de aplicativos, selecione **Druva**.</span><span class="sxs-lookup"><span data-stu-id="24c12-249">In the applications list, select **Druva**.</span></span>

    ![O link do Druva na lista de Aplicativos](./media/active-directory-saas-druva-tutorial/tutorial_druva_app.png)  

3. <span data-ttu-id="24c12-251">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="24c12-251">In the menu on the left, click **Users and groups**.</span></span>

    ![O link “Usuários e grupos”][202]

4. <span data-ttu-id="24c12-253">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="24c12-253">Click **Add** button.</span></span> <span data-ttu-id="24c12-254">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="24c12-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![O painel Adicionar Atribuição][203]

5. <span data-ttu-id="24c12-256">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="24c12-256">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="24c12-257">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="24c12-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="24c12-258">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="24c12-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="24c12-259">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="24c12-259">Test single sign-on</span></span>

<span data-ttu-id="24c12-260">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="24c12-260">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="24c12-261">Ao clicar no bloco do Druva no Painel de Acesso, você deverá ser conectado automaticamente ao aplicativo Druva.</span><span class="sxs-lookup"><span data-stu-id="24c12-261">When you click the Druva tile in the Access Panel, you should get automatically signed-on to your Druva application.</span></span>
<span data-ttu-id="24c12-262">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="24c12-262">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="24c12-263">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="24c12-263">Additional resources</span></span>

* [<span data-ttu-id="24c12-264">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="24c12-264">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="24c12-265">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="24c12-265">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-druva-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-druva-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-druva-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-druva-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-druva-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-druva-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-druva-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-druva-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-druva-tutorial/tutorial_general_203.png

