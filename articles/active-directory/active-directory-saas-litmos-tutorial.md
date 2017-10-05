---
title: "Tutorial: Integração do Azure Active Directory ao Litmos | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Active Directory do Azure e o Litmos."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: jeedes
ms.assetid: cfaae4bb-e8e5-41d1-ac88-8cc369653036
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: ef1b5860ba0a406022bbd11afb366d14bee2c57d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-litmos"></a><span data-ttu-id="939af-103">Tutorial: Integração do Active Directory do Azure ao Litmos</span><span class="sxs-lookup"><span data-stu-id="939af-103">Tutorial: Azure Active Directory integration with Litmos</span></span>

<span data-ttu-id="939af-104">Neste tutorial, você aprende a integrar o Litmos ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="939af-104">In this tutorial, you learn how to integrate Litmos with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="939af-105">A integração do Litmos ao Azure AD proporciona os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="939af-105">Integrating Litmos with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="939af-106">No Azure AD, é possível controlar quem tem acesso ao Litmos.</span><span class="sxs-lookup"><span data-stu-id="939af-106">You can control in Azure AD who has access to Litmos.</span></span>
- <span data-ttu-id="939af-107">É possível permitir que os usuários se conectem automaticamente ao Litmos (Logon Único) com suas contas do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="939af-107">You can enable your users to automatically get signed-on to Litmos (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="939af-108">Você pode gerenciar suas contas em um único local central – o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="939af-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="939af-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="939af-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="939af-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="939af-110">Prerequisites</span></span>

<span data-ttu-id="939af-111">Para configurar a integração do AD do Azure ao Litmos, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="939af-111">To configure Azure AD integration with Litmos, you need the following items:</span></span>

- <span data-ttu-id="939af-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="939af-112">An Azure AD subscription</span></span>
- <span data-ttu-id="939af-113">Uma assinatura habilitada para logon único do Litmos</span><span class="sxs-lookup"><span data-stu-id="939af-113">A Litmos single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="939af-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="939af-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="939af-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="939af-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="939af-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="939af-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="939af-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="939af-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="939af-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="939af-118">Scenario description</span></span>
<span data-ttu-id="939af-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="939af-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="939af-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="939af-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="939af-121">Adicionando o Litmos da galeria</span><span class="sxs-lookup"><span data-stu-id="939af-121">Adding Litmos from the gallery</span></span>
2. <span data-ttu-id="939af-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="939af-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-litmos-from-the-gallery"></a><span data-ttu-id="939af-123">Adicionando o Litmos da galeria</span><span class="sxs-lookup"><span data-stu-id="939af-123">Adding Litmos from the gallery</span></span>
<span data-ttu-id="939af-124">Para configurar a integração do Litmos ao AD do Azure, você precisará adicionar o Litmos da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="939af-124">To configure the integration of Litmos into Azure AD, you need to add Litmos from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="939af-125">**Para adicionar o Litmos da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="939af-125">**To add Litmos from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="939af-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="939af-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![O botão Azure Active Directory][1]

2. <span data-ttu-id="939af-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="939af-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="939af-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="939af-129">Then go to **All applications**.</span></span>

    ![A folha Aplicativos empresariais][2]
    
3. <span data-ttu-id="939af-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="939af-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![O botão Novo aplicativo][3]

4. <span data-ttu-id="939af-133">Na caixa de pesquisa, digite **Litmos**, selecione **Litmos** no painel de resultados e, depois, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="939af-133">In the search box, type **Litmos**, select **Litmos** from result panel then click **Add** button to add the application.</span></span>

    ![Litmos na lista de resultados](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="939af-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="939af-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="939af-136">Nesta seção, você configura e testa o logon único do Azure AD com o Litmos, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="939af-136">In this section, you configure and test Azure AD single sign-on with Litmos based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="939af-137">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Litmos é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="939af-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Litmos is to a user in Azure AD.</span></span> <span data-ttu-id="939af-138">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Litmos.</span><span class="sxs-lookup"><span data-stu-id="939af-138">In other words, a link relationship between an Azure AD user and the related user in Litmos needs to be established.</span></span>

<span data-ttu-id="939af-139">No Litmos, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="939af-139">In Litmos, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="939af-140">Para configurar e testar o logon único do AD do Azure com o Litmos, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="939af-140">To configure and test Azure AD single sign-on with Litmos, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="939af-141">**[Configurar o logon único do Azure AD](#configure-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="939af-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="939af-142">**[Criar um usuário de teste do Azure AD](#create-an-azure-ad-test-user)** – para testar o logon único do Azure AD com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="939af-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="939af-143">**[Criar um usuário de teste do Litmos](#create-a-litmos-test-user)** – para ter um equivalente de Brenda Fernandes no Litmos que esteja vinculado à representação de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="939af-143">**[Create a Litmos test user](#create-a-litmos-test-user)** - to have a counterpart of Britta Simon in Litmos that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="939af-144">**[Atribuir o usuário de teste do Azure AD](#assign-the-azure-ad-test-user)** – para permitir que Brenda Fernandes use o logon único do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="939af-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="939af-145">**[Teste o logon único](#test-single-sign-on)** – para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="939af-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="939af-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="939af-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="939af-147">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo Litmos.</span><span class="sxs-lookup"><span data-stu-id="939af-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Litmos application.</span></span>

<span data-ttu-id="939af-148">**Para configurar o logon único do AD do Azure com o Litmos, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="939af-148">**To configure Azure AD single sign-on with Litmos, perform the following steps:**</span></span>

1. <span data-ttu-id="939af-149">No portal do Azure, na página de integração do aplicativo **Litmos**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="939af-149">In the Azure portal, on the **Litmos** application integration page, click **Single sign-on**.</span></span>

    ![Link Configurar logon único][4]

2. <span data-ttu-id="939af-151">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="939af-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_samlbase.png)

3. <span data-ttu-id="939af-153">Na seção **Domínio e URLs do Litmos**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="939af-153">On the **Litmos Domain and URLs** section, perform the following steps:</span></span>

    ![Informações de logon único em Domínio e URLs do Litmos](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_url.png)

    <span data-ttu-id="939af-155">a.</span><span class="sxs-lookup"><span data-stu-id="939af-155">a.</span></span> <span data-ttu-id="939af-156">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<companyname>.litmos.com/account/Login`</span><span class="sxs-lookup"><span data-stu-id="939af-156">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.litmos.com/account/Login`</span></span>

    <span data-ttu-id="939af-157">b.</span><span class="sxs-lookup"><span data-stu-id="939af-157">b.</span></span> <span data-ttu-id="939af-158">Na caixa de texto **URL de resposta**, digite uma URL no seguinte padrão: `https://<companyname>.litmos.com/integration/samllogin`</span><span class="sxs-lookup"><span data-stu-id="939af-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyname>.litmos.com/integration/samllogin`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="939af-159">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="939af-159">These values are not real.</span></span> <span data-ttu-id="939af-160">Atualize esses valores com o Identificador e a URL de Resposta reais, que são explicados adiante no tutorial ou contate a [equipe de suporte do Litmos](https://www.litmos.com/contact-us/) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="939af-160">Update these values with the actual Identifier and Reply URL, which are explained later in tutorial or contact [Litmos support team](https://www.litmos.com/contact-us/) to get these values.</span></span>

4. <span data-ttu-id="939af-161">Na seção **Certificado de Autenticação do SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado no computador.</span><span class="sxs-lookup"><span data-stu-id="939af-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![O link de download do Certificado](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_certificate.png)

5. <span data-ttu-id="939af-163">Como parte da configuração, você precisa personalizar os **Atributos de Token SAML** para seu aplicativo Litmos.</span><span class="sxs-lookup"><span data-stu-id="939af-163">As part of the configuration, you need to customize the **SAML Token Attributes** for your Litmos application.</span></span>

    ![Seção Atributo](./media/active-directory-saas-litmos-tutorial/tutorial_attribute.png)
           
    | <span data-ttu-id="939af-165">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="939af-165">Attribute Name</span></span>   | <span data-ttu-id="939af-166">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="939af-166">Attribute Value</span></span> |   
    | ---------------  | ----------------|
    | <span data-ttu-id="939af-167">Nome</span><span class="sxs-lookup"><span data-stu-id="939af-167">FirstName</span></span> |<span data-ttu-id="939af-168">user.givenname</span><span class="sxs-lookup"><span data-stu-id="939af-168">user.givenname</span></span> |
    | <span data-ttu-id="939af-169">Sobrenome</span><span class="sxs-lookup"><span data-stu-id="939af-169">LastName</span></span>  |<span data-ttu-id="939af-170">user.surname</span><span class="sxs-lookup"><span data-stu-id="939af-170">user.surname</span></span> |
    | <span data-ttu-id="939af-171">Email</span><span class="sxs-lookup"><span data-stu-id="939af-171">Email</span></span> |<span data-ttu-id="939af-172">user.mail</span><span class="sxs-lookup"><span data-stu-id="939af-172">user.mail</span></span> |

    <span data-ttu-id="939af-173">a.</span><span class="sxs-lookup"><span data-stu-id="939af-173">a.</span></span> <span data-ttu-id="939af-174">Clique em **Adicionar atributo** para abrir o diálogo **Adicionar Atributo**.</span><span class="sxs-lookup"><span data-stu-id="939af-174">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Adicionar atributo](./media/active-directory-saas-litmos-tutorial/tutorial_attribute_04.png)

    ![Caixa de diálogo Adicionar atributo](./media/active-directory-saas-litmos-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="939af-177">b.</span><span class="sxs-lookup"><span data-stu-id="939af-177">b.</span></span> <span data-ttu-id="939af-178">Na caixa de texto **Nome** , digite o nome do atributo mostrado para essa linha.</span><span class="sxs-lookup"><span data-stu-id="939af-178">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="939af-179">c.</span><span class="sxs-lookup"><span data-stu-id="939af-179">c.</span></span> <span data-ttu-id="939af-180">Na lista **Valor**, digite o valor do atributo mostrado para essa linha.</span><span class="sxs-lookup"><span data-stu-id="939af-180">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="939af-181">d.</span><span class="sxs-lookup"><span data-stu-id="939af-181">d.</span></span> <span data-ttu-id="939af-182">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="939af-182">Click **Ok**.</span></span>     

6. <span data-ttu-id="939af-183">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="939af-183">Click **Save** button.</span></span>

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-litmos-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="939af-185">Em outra janela do navegador, entre em seu site de empresa do Litmos como administrador.</span><span class="sxs-lookup"><span data-stu-id="939af-185">In a different browser window, sign-on to your Litmos company site as administrator.</span></span>

8. <span data-ttu-id="939af-186">Na barra de navegação à esquerda, clique em **Contas**.</span><span class="sxs-lookup"><span data-stu-id="939af-186">In the navigation bar on the left side, click **Accounts**.</span></span>
   
    ![Seção Contas no lado do aplicativo][22] 

9. <span data-ttu-id="939af-188">Clique na guia **Integrações** .</span><span class="sxs-lookup"><span data-stu-id="939af-188">Click the **Integrations** tab.</span></span>
   
    ![Guia Integração][23] 

10. <span data-ttu-id="939af-190">Na guia **Integrações**, role para baixo até **Integrações de Terceiros** e clique na guia **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="939af-190">On the **Integrations** tab, scroll down to **3rd Party Integrations**, and then click **SAML 2.0** tab.</span></span>
   
    ![Seção SAML 2.0][24] 

11. <span data-ttu-id="939af-192">Copie o valor em **O ponto de extremidade SAML do Litmos é:** e cole-o na caixa de texto **URL de Resposta** na seção **Domínio e URLs do Litmos** do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="939af-192">Copy the value under **The SAML endpoint for litmos is:** and paste it into the **Reply URL** textbox in the **Litmos Domain and URLs** section in Azure portal.</span></span> 
   
    ![Ponto de extremidade SAML][26] 

12. <span data-ttu-id="939af-194">No seu aplicativo **Litmos** , execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="939af-194">In your **Litmos** application, perform the following steps:</span></span>
    
     ![Aplicativo Litmos][25] 
     
     <span data-ttu-id="939af-196">a.</span><span class="sxs-lookup"><span data-stu-id="939af-196">a.</span></span> <span data-ttu-id="939af-197">Clique em **Habilitar SAML**.</span><span class="sxs-lookup"><span data-stu-id="939af-197">Click **Enable SAML**.</span></span>
    
     <span data-ttu-id="939af-198">b.</span><span class="sxs-lookup"><span data-stu-id="939af-198">b.</span></span> <span data-ttu-id="939af-199">Abra seu certificado codificado em base 64 no bloco de notas, copie o conteúdo dele para a área de transferência e cole-o na caixa de texto **Certificado SAML X.509** .</span><span class="sxs-lookup"><span data-stu-id="939af-199">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **SAML X.509 Certificate** textbox.</span></span>
     
     <span data-ttu-id="939af-200">c.</span><span class="sxs-lookup"><span data-stu-id="939af-200">c.</span></span> <span data-ttu-id="939af-201">Clique em **Salvar Alterações**.</span><span class="sxs-lookup"><span data-stu-id="939af-201">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="939af-202">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="939af-202">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="939af-203">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="939af-203">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="939af-204">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="939af-204">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="939af-205">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="939af-205">Create an Azure AD test user</span></span>

<span data-ttu-id="939af-206">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="939af-206">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Criar um usuário de teste do Azure AD][100]

<span data-ttu-id="939af-208">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="939af-208">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="939af-209">No portal do Azure, no painel esquerdo, clique no botão **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="939af-209">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![O botão Azure Active Directory](./media/active-directory-saas-litmos-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="939af-211">Para exibir a lista de usuários, acesse **Usuários e grupos** e, depois, clique em **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="939af-211">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Os links “Usuários e grupos” e “Todos os usuários”](./media/active-directory-saas-litmos-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="939af-213">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo **Todos os Usuários**.</span><span class="sxs-lookup"><span data-stu-id="939af-213">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![O botão Adicionar](./media/active-directory-saas-litmos-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="939af-215">Na caixa de diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="939af-215">In the **User** dialog box, perform the following steps:</span></span>

    ![A caixa de diálogo Usuário](./media/active-directory-saas-litmos-tutorial/create_aaduser_04.png)

    <span data-ttu-id="939af-217">a.</span><span class="sxs-lookup"><span data-stu-id="939af-217">a.</span></span> <span data-ttu-id="939af-218">Na caixa **Nome**, digite **BrendaFernandes**.</span><span class="sxs-lookup"><span data-stu-id="939af-218">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="939af-219">b.</span><span class="sxs-lookup"><span data-stu-id="939af-219">b.</span></span> <span data-ttu-id="939af-220">Na caixa **Nome de usuário**, digite o endereço de email do usuário Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="939af-220">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="939af-221">c.</span><span class="sxs-lookup"><span data-stu-id="939af-221">c.</span></span> <span data-ttu-id="939af-222">Marque a caixa de seleção **Mostrar Senha** e, em seguida, anote o valor exibido na caixa **Senha**.</span><span class="sxs-lookup"><span data-stu-id="939af-222">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="939af-223">d.</span><span class="sxs-lookup"><span data-stu-id="939af-223">d.</span></span> <span data-ttu-id="939af-224">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="939af-224">Click **Create**.</span></span>
  
### <a name="create-a-litmos-test-user"></a><span data-ttu-id="939af-225">Criar um usuário de teste do Litmos</span><span class="sxs-lookup"><span data-stu-id="939af-225">Create a Litmos test user</span></span>

<span data-ttu-id="939af-226">O objetivo desta seção é criar um usuário chamado Brenda Fernandes no Litmos.</span><span class="sxs-lookup"><span data-stu-id="939af-226">The objective of this section is to create a user called Britta Simon in Litmos.</span></span>  
<span data-ttu-id="939af-227">O aplicativo Litmos oferece suporte ao provisionamento Just-in-Time.</span><span class="sxs-lookup"><span data-stu-id="939af-227">The Litmos application supports Just-in-Time provisioning.</span></span> <span data-ttu-id="939af-228">Isso significa que, se for necessário, uma conta de usuário será criada automaticamente durante uma tentativa de acessar o aplicativo usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="939af-228">This means, a user account is automatically created if necessary during an attempt to access the application using the Access Panel.</span></span>

<span data-ttu-id="939af-229">**Para criar um usuário chamado Brenda Fernandes no Litmos, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="939af-229">**To create a user called Britta Simon in Litmos, perform the following steps:**</span></span>

1. <span data-ttu-id="939af-230">Em outra janela do navegador, entre em seu site de empresa do Litmos como administrador.</span><span class="sxs-lookup"><span data-stu-id="939af-230">In a different browser window, sign-on to your Litmos company site as administrator.</span></span>

2. <span data-ttu-id="939af-231">Na barra de navegação à esquerda, clique em **Contas**.</span><span class="sxs-lookup"><span data-stu-id="939af-231">In the navigation bar on the left side, click **Accounts**.</span></span>
   
    ![Seção Contas no lado do aplicativo][22] 

3. <span data-ttu-id="939af-233">Clique na guia **Integrações** .</span><span class="sxs-lookup"><span data-stu-id="939af-233">Click the **Integrations** tab.</span></span>
   
    ![Guia Integrações][23] 

4. <span data-ttu-id="939af-235">Na guia **Integrações**, role para baixo até **Integrações de Terceiros** e clique na guia **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="939af-235">On the **Integrations** tab, scroll down to **3rd Party Integrations**, and then click **SAML 2.0** tab.</span></span>
   
    ![SAML 2.0][24] 
    
5. <span data-ttu-id="939af-237">Selecione **Gerar Usuários Automaticamente**</span><span class="sxs-lookup"><span data-stu-id="939af-237">Select **Autogenerate Users**</span></span>
   
    ![Gerar usuários automaticamente][27] 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="939af-239">Atribuir o usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="939af-239">Assign the Azure AD test user</span></span>

<span data-ttu-id="939af-240">Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo acesso ao Litmos.</span><span class="sxs-lookup"><span data-stu-id="939af-240">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Litmos.</span></span>

![Atribuir a função de usuário][200] 

<span data-ttu-id="939af-242">**Para atribuir Brenda Fernandes ao Litmos, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="939af-242">**To assign Britta Simon to Litmos, perform the following steps:**</span></span>

1. <span data-ttu-id="939af-243">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="939af-243">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="939af-245">Na lista de aplicativos, escolha **Litmos**.</span><span class="sxs-lookup"><span data-stu-id="939af-245">In the applications list, select **Litmos**.</span></span>

    ![O link do Litmos na lista de Aplicativos](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_app.png)  

3. <span data-ttu-id="939af-247">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="939af-247">In the menu on the left, click **Users and groups**.</span></span>

    ![O link “Usuários e grupos”][202]

4. <span data-ttu-id="939af-249">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="939af-249">Click **Add** button.</span></span> <span data-ttu-id="939af-250">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="939af-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![O painel Adicionar Atribuição][203]

5. <span data-ttu-id="939af-252">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="939af-252">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="939af-253">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="939af-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="939af-254">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="939af-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="939af-255">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="939af-255">Test single sign-on</span></span>

<span data-ttu-id="939af-256">O objetivo desta seção é testar sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="939af-256">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  

<span data-ttu-id="939af-257">Ao clicar no bloco Litmos no Painel de Acesso, você deverá ser conectado automaticamente ao seu aplicativo Litmos.</span><span class="sxs-lookup"><span data-stu-id="939af-257">When you click the Litmos tile in the Access Panel, you should get automatically signed-on to your Litmos application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="939af-258">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="939af-258">Additional resources</span></span>

* [<span data-ttu-id="939af-259">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="939af-259">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="939af-260">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="939af-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_04.png
[21]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_60.png
[22]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_61.png
[23]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_62.png
[24]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_63.png
[25]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_64.png
[26]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_65.png
[27]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_66.png

[100]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_203.png

