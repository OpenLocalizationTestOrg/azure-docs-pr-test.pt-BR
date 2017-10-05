---
title: "Tutorial: integração do Azure Active Directory ao Front | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Front."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 88270b6d-2571-434a-b139-b6ccc3a2b19f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: d936bc50a66ac2a3c17038ff08351edf9902c99f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-front"></a><span data-ttu-id="875a4-103">Tutorial: integração do Azure Active Directory ao Front</span><span class="sxs-lookup"><span data-stu-id="875a4-103">Tutorial: Azure Active Directory integration with Front</span></span>

<span data-ttu-id="875a4-104">Neste tutorial, você aprenderá a integrar o Front ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="875a4-104">In this tutorial, you learn how to integrate Front with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="875a4-105">A integração do Front ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="875a4-105">Integrating Front with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="875a4-106">No Azure AD, é possível controlar quem tem acesso ao Front.</span><span class="sxs-lookup"><span data-stu-id="875a4-106">You can control in Azure AD who has access to Front.</span></span>
- <span data-ttu-id="875a4-107">Você pode permitir que seus usuários façam logon automaticamente no Front (logon único) com suas contas do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="875a4-107">You can enable your users to automatically get signed-on to Front (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="875a4-108">Você pode gerenciar suas contas em um único local central – o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="875a4-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="875a4-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="875a4-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="875a4-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="875a4-110">Prerequisites</span></span>

<span data-ttu-id="875a4-111">Para configurar a integração do Azure AD ao Front, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="875a4-111">To configure Azure AD integration with Front, you need the following items:</span></span>

- <span data-ttu-id="875a4-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="875a4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="875a4-113">Uma assinatura de Front habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="875a4-113">A Front single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="875a4-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="875a4-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="875a4-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="875a4-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="875a4-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="875a4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="875a4-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="875a4-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="875a4-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="875a4-118">Scenario description</span></span>
<span data-ttu-id="875a4-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="875a4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="875a4-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="875a4-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="875a4-121">Adição do Front por meio da Galeria</span><span class="sxs-lookup"><span data-stu-id="875a4-121">Adding Front from the gallery</span></span>
2. <span data-ttu-id="875a4-122">configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="875a4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-front-from-the-gallery"></a><span data-ttu-id="875a4-123">Adição do Front por meio da Galeria</span><span class="sxs-lookup"><span data-stu-id="875a4-123">Adding Front from the gallery</span></span>
<span data-ttu-id="875a4-124">Para configurar a integração do Front ao Azure AD, você precisa adicionar o Front por meio da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="875a4-124">To configure the integration of Front into Azure AD, you need to add Front from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="875a4-125">**Para adicionar o Front por meio da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="875a4-125">**To add Front from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="875a4-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="875a4-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![O botão Azure Active Directory][1]

2. <span data-ttu-id="875a4-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="875a4-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="875a4-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="875a4-129">Then go to **All applications**.</span></span>

    ![A folha Aplicativos empresariais][2]
    
3. <span data-ttu-id="875a4-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="875a4-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![O botão Novo aplicativo][3]

4. <span data-ttu-id="875a4-133">Na caixa de pesquisa, digite **Front**, selecione **Front** no painel de resultados e, em seguida, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="875a4-133">In the search box, type **Front**, select **Front** from result panel then click **Add** button to add the application.</span></span>

    ![Front na lista de resultados](./media/active-directory-saas-front-tutorial/tutorial_front_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="875a4-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="875a4-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="875a4-136">Nesta seção, você configurará e testará o logon único do Azure AD com o Front, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="875a4-136">In this section, you configure and test Azure AD single sign-on with Front based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="875a4-137">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Front é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="875a4-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Front is to a user in Azure AD.</span></span> <span data-ttu-id="875a4-138">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Front.</span><span class="sxs-lookup"><span data-stu-id="875a4-138">In other words, a link relationship between an Azure AD user and the related user in Front needs to be established.</span></span>

<span data-ttu-id="875a4-139">No Front, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="875a4-139">In Front, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="875a4-140">Para configurar e testar o logon único do Azure AD com o Front, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="875a4-140">To configure and test Azure AD single sign-on with Front, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="875a4-141">**[Configurar o logon único do Azure AD](#configure-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="875a4-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="875a4-142">**[Criar um usuário de teste do Azure AD](#create-an-azure-ad-test-user)** – para testar o logon único do Azure AD com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="875a4-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="875a4-143">**[Criar de um usuário de teste do Front](#create-a-front-test-user)** : para ter um equivalente de Brenda Fernandes no Front que esteja vinculado à representação de usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="875a4-143">**[Create a Front test user](#create-a-front-test-user)** - to have a counterpart of Britta Simon in Front that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="875a4-144">**[Atribuir o usuário de teste do Azure AD](#assign-the-azure-ad-test-user)** – para permitir que Brenda Fernandes use o logon único do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="875a4-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="875a4-145">**[Teste o logon único](#test-single-sign-on)** – para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="875a4-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="875a4-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="875a4-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="875a4-147">Nesta seção, você habilitará o logon único do Azure AD no portal do Azure e configurará o logon único em seu aplicativo Front.</span><span class="sxs-lookup"><span data-stu-id="875a4-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Front application.</span></span>

<span data-ttu-id="875a4-148">**Para configurar o logon único do Azure AD com o Front, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="875a4-148">**To configure Azure AD single sign-on with Front, perform the following steps:**</span></span>

1. <span data-ttu-id="875a4-149">No portal do Azure, na página de integração do aplicativo **Front**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="875a4-149">In the Azure portal, on the **Front** application integration page, click **Single sign-on**.</span></span>

    ![Link Configurar logon único][4]

2. <span data-ttu-id="875a4-151">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="875a4-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-front-tutorial/tutorial_front_samlbase.png)

3. <span data-ttu-id="875a4-153">Na seção **Domínio e URLs do Front**, se desejar configurar o aplicativo no modo iniciado pelo **IDP**:</span><span class="sxs-lookup"><span data-stu-id="875a4-153">On the **Front Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-front-tutorial/tutorial_front_url1.png)

    <span data-ttu-id="875a4-155">a.</span><span class="sxs-lookup"><span data-stu-id="875a4-155">a.</span></span> <span data-ttu-id="875a4-156">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<companyname>.frontapp.com`</span><span class="sxs-lookup"><span data-stu-id="875a4-156">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.frontapp.com`</span></span>

    <span data-ttu-id="875a4-157">b.</span><span class="sxs-lookup"><span data-stu-id="875a4-157">b.</span></span> <span data-ttu-id="875a4-158">Na caixa de texto **URL de resposta**, digite uma URL no seguinte padrão: `https://<companyname>.frontapp.com/sso/saml/callback`</span><span class="sxs-lookup"><span data-stu-id="875a4-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyname>.frontapp.com/sso/saml/callback`</span></span>

4. <span data-ttu-id="875a4-159">Marque **Mostrar configurações avançadas de URL** se quiser configurar o aplicativo no modo iniciado em **SP**:</span><span class="sxs-lookup"><span data-stu-id="875a4-159">Check **Show advanced URL settings**, If you wish to configure the application in **SP** initiated mode:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-front-tutorial/tutorial_front_url2.png)

    <span data-ttu-id="875a4-161">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<companyname>.frontapp.com`</span><span class="sxs-lookup"><span data-stu-id="875a4-161">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.frontapp.com`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="875a4-162">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="875a4-162">These values are not real.</span></span> <span data-ttu-id="875a4-163">Atualize esses valores com o Identificador, a URL de Resposta e a URL de Logon reais, que são explicados adiante no tutorial ou contate a [equipe de suporte do Front Client](mailto:support@frontapp.com) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="875a4-163">Update these values with the actual Identifier, Reply URL, and Sign-On URL which are explained later in tutorial or contact [Front Client support team](mailto:support@frontapp.com) to get these values.</span></span> 

5. <span data-ttu-id="875a4-164">Na seção **Certificado de Autenticação do SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado no computador.</span><span class="sxs-lookup"><span data-stu-id="875a4-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-front-tutorial/tutorial_front_certificate.png) 

6. <span data-ttu-id="875a4-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="875a4-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-front-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="875a4-168">Na seção **Configuração do Front**, clique em **Configurar Front** para abrir a janela **Configurar Logon**.</span><span class="sxs-lookup"><span data-stu-id="875a4-168">On the **Front Configuration** section, click **Configure Front** to open **Configure sign-on** window.</span></span> <span data-ttu-id="875a4-169">Copie a **URL de saída, a ID da Entidade SAML e a URL do Serviço de Logon Único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="875a4-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-front-tutorial/tutorial_front_configure.png) 

8. <span data-ttu-id="875a4-171">Faça logon no seu locatário do Front como administrador.</span><span class="sxs-lookup"><span data-stu-id="875a4-171">Sign-on to your Front tenant as an administrator.</span></span>

9. <span data-ttu-id="875a4-172">Acesse as **Configurações (ícone de engrenagem na parte inferior da barra lateral esquerda) > Preferências**.</span><span class="sxs-lookup"><span data-stu-id="875a4-172">Go to **Settings (cog icon at the bottom of the left sidebar) > Preferences**.</span></span>
   
    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-front-tutorial/tutorial_front_000.png)

10. <span data-ttu-id="875a4-174">Clique no link **Logon Único** .</span><span class="sxs-lookup"><span data-stu-id="875a4-174">Click **Single Sign On** link.</span></span>
   
    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-front-tutorial/tutorial_front_001.png)

11. <span data-ttu-id="875a4-176">Selecione **SAML** na lista suspensa do **Logon Único**.</span><span class="sxs-lookup"><span data-stu-id="875a4-176">Select **SAML** in the drop-down list of **Single Sign On**.</span></span>
   
    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-front-tutorial/tutorial_front_002.png)

12. <span data-ttu-id="875a4-178">Na caixa de texto **Ponto de Entrada**, insira o valor da **URL de serviço de logon único** do assistente de configuração de aplicativo do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="875a4-178">In the **Entry Point** textbox put the value of **Single Sign-on Service URL** from Azure AD application configuration wizard.</span></span>
    
    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-front-tutorial/tutorial_front_003.png)

13. <span data-ttu-id="875a4-180">Abra o arquivo de **Certificado (Base64)** baixado no bloco de notas, copie o conteúdo dele para a área de transferência e, depois, cole-o na caixa de texto **Certificado de autenticação**.</span><span class="sxs-lookup"><span data-stu-id="875a4-180">Open your downloaded **Certificate(Base64)** file in notepad, copy the content of it into your clipboard, and then paste it to the **Signing certificate** textbox.</span></span>
    
    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-front-tutorial/tutorial_front_004.png)

14. <span data-ttu-id="875a4-182">Na seção de **Configurações de provedores de serviço**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="875a4-182">On the **Service provider settings** section, perform the following steps:</span></span>

    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-front-tutorial/tutorial_front_005.png)

    <span data-ttu-id="875a4-184">a.</span><span class="sxs-lookup"><span data-stu-id="875a4-184">a.</span></span> <span data-ttu-id="875a4-185">Copie o valor da **ID da entidade** e cole-o na caixa de texto **Identificador**, na seção **Domínio e URLs do Front** no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="875a4-185">Copy the value of **Entity ID** and paste it into the **Identifier** textbox in **Front Domain and URLs** section in Azure portal.</span></span>

    <span data-ttu-id="875a4-186">b.</span><span class="sxs-lookup"><span data-stu-id="875a4-186">b.</span></span> <span data-ttu-id="875a4-187">Copie o valor da **URL do ACS** e cole-o na caixa de texto **URL de Logon**, na seção **Domínio e URLs do Front** no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="875a4-187">Copy the value of **ACS URL** and paste it into the **Sign-on URL** textbox in **Front Domain and URLs** section in Azure portal.</span></span>
    
15. <span data-ttu-id="875a4-188">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="875a4-188">Click **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="875a4-189">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="875a4-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="875a4-190">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="875a4-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="875a4-191">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="875a4-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="875a4-192">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="875a4-192">Create an Azure AD test user</span></span>

<span data-ttu-id="875a4-193">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="875a4-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Criar um usuário de teste do Azure AD][100]

<span data-ttu-id="875a4-195">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="875a4-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="875a4-196">No portal do Azure, no painel esquerdo, clique no botão **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="875a4-196">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![O botão Azure Active Directory](./media/active-directory-saas-front-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="875a4-198">Para exibir a lista de usuários, acesse **Usuários e grupos** e, depois, clique em **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="875a4-198">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Os links “Usuários e grupos” e “Todos os usuários”](./media/active-directory-saas-front-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="875a4-200">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo **Todos os Usuários**.</span><span class="sxs-lookup"><span data-stu-id="875a4-200">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![O botão Adicionar](./media/active-directory-saas-front-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="875a4-202">Na caixa de diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="875a4-202">In the **User** dialog box, perform the following steps:</span></span>

    ![A caixa de diálogo Usuário](./media/active-directory-saas-front-tutorial/create_aaduser_04.png)

    <span data-ttu-id="875a4-204">a.</span><span class="sxs-lookup"><span data-stu-id="875a4-204">a.</span></span> <span data-ttu-id="875a4-205">Na caixa **Nome**, digite **BrendaFernandes**.</span><span class="sxs-lookup"><span data-stu-id="875a4-205">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="875a4-206">b.</span><span class="sxs-lookup"><span data-stu-id="875a4-206">b.</span></span> <span data-ttu-id="875a4-207">Na caixa **Nome de usuário**, digite o endereço de email do usuário Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="875a4-207">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="875a4-208">c.</span><span class="sxs-lookup"><span data-stu-id="875a4-208">c.</span></span> <span data-ttu-id="875a4-209">Marque a caixa de seleção **Mostrar Senha** e, em seguida, anote o valor exibido na caixa **Senha**.</span><span class="sxs-lookup"><span data-stu-id="875a4-209">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="875a4-210">d.</span><span class="sxs-lookup"><span data-stu-id="875a4-210">d.</span></span> <span data-ttu-id="875a4-211">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="875a4-211">Click **Create**.</span></span>
 
### <a name="create-a-front-test-user"></a><span data-ttu-id="875a4-212">Criar um usuário de teste do Front</span><span class="sxs-lookup"><span data-stu-id="875a4-212">Create a Front test user</span></span>

<span data-ttu-id="875a4-213">Nesta seção, você criará uma usuária chamada Britta Simon no Front.</span><span class="sxs-lookup"><span data-stu-id="875a4-213">In this section, you create a user called Britta Simon in Front.</span></span> <span data-ttu-id="875a4-214">Trabalhe com a [equipe de suporte ao Cliente do Front](mailto:support@frontapp.com) para adicionar os usuários à plataforma Front.</span><span class="sxs-lookup"><span data-stu-id="875a4-214">Work with [Front Client support team](mailto:support@frontapp.com) to add the users in the Front platform.</span></span> <span data-ttu-id="875a4-215">Os usuários devem ser criados e ativados antes de usar o logon único.</span><span class="sxs-lookup"><span data-stu-id="875a4-215">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="875a4-216">Atribuir o usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="875a4-216">Assign the Azure AD test user</span></span>

<span data-ttu-id="875a4-217">Nesta seção, você permitirá que Britta Simon use o logon único do Azure concedendo-lhe acesso ao Front.</span><span class="sxs-lookup"><span data-stu-id="875a4-217">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Front.</span></span>

![Atribuir a função de usuário][200] 

<span data-ttu-id="875a4-219">**Para atribuir Brenda Fernandes ao Front, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="875a4-219">**To assign Britta Simon to Front, perform the following steps:**</span></span>

1. <span data-ttu-id="875a4-220">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="875a4-220">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="875a4-222">Na lista de aplicativos, escolha **Fuse**.</span><span class="sxs-lookup"><span data-stu-id="875a4-222">In the applications list, select **Front**.</span></span>

    ![O link do Front na lista de Aplicativos](./media/active-directory-saas-front-tutorial/tutorial_front_app.png)  

3. <span data-ttu-id="875a4-224">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="875a4-224">In the menu on the left, click **Users and groups**.</span></span>

    ![O link “Usuários e grupos”][202]

4. <span data-ttu-id="875a4-226">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="875a4-226">Click **Add** button.</span></span> <span data-ttu-id="875a4-227">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="875a4-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![O painel Adicionar Atribuição][203]

5. <span data-ttu-id="875a4-229">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="875a4-229">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="875a4-230">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="875a4-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="875a4-231">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="875a4-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="875a4-232">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="875a4-232">Test single sign-on</span></span>

<span data-ttu-id="875a4-233">O objetivo desta seção é testar sua configuração de SSO do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="875a4-233">The objective of this section is to test your Azure AD SSOconfiguration using the Access Panel.</span></span>

<span data-ttu-id="875a4-234">Ao clicar no bloco do Front no Painel de Acesso, você deverá ser conectado automaticamente ao seu aplicativo Front.</span><span class="sxs-lookup"><span data-stu-id="875a4-234">When you click the Front tile in the Access Panel, you should get automatically signed-on to your Front application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="875a4-235">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="875a4-235">Additional resources</span></span>

* [<span data-ttu-id="875a4-236">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="875a4-236">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="875a4-237">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="875a4-237">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-front-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-front-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-front-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-front-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-front-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-front-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-front-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-front-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-front-tutorial/tutorial_general_203.png

