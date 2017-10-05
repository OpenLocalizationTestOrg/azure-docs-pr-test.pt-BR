---
title: "Tutorial: Integração do Azure Active Directory ao Clever | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Clever."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 069ff13a-310e-4366-a147-d6ec5cca12a5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 84082ff567e37d7fff80be9e089c67cfab911861
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-clever"></a><span data-ttu-id="c5867-103">Tutorial: integração do Active Directory do Azure ao Clever</span><span class="sxs-lookup"><span data-stu-id="c5867-103">Tutorial: Azure Active Directory integration with Clever</span></span>

<span data-ttu-id="c5867-104">Neste tutorial, você aprende a integrar o Clever ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="c5867-104">In this tutorial, you learn how to integrate Clever with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c5867-105">A integração do Clever ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="c5867-105">Integrating Clever with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c5867-106">No Azure AD, é possível controlar quem tem acesso ao Clever.</span><span class="sxs-lookup"><span data-stu-id="c5867-106">You can control in Azure AD who has access to Clever.</span></span>
- <span data-ttu-id="c5867-107">Você pode permitir que usuários façam logon automaticamente no Clever (logon único) com as respectivas contas do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="c5867-107">You can enable your users to automatically get signed-on to Clever (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="c5867-108">Você pode gerenciar suas contas em um único local central – o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c5867-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="c5867-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c5867-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c5867-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="c5867-110">Prerequisites</span></span>

<span data-ttu-id="c5867-111">Para configurar a integração do Azure AD ao Clever, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="c5867-111">To configure Azure AD integration with Clever, you need the following items:</span></span>

- <span data-ttu-id="c5867-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c5867-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c5867-113">Uma assinatura do Clever habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="c5867-113">A Clever single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c5867-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="c5867-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c5867-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="c5867-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c5867-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="c5867-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c5867-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c5867-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c5867-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="c5867-118">Scenario description</span></span>
<span data-ttu-id="c5867-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="c5867-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c5867-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="c5867-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c5867-121">Adicionando o Clever da galeria</span><span class="sxs-lookup"><span data-stu-id="c5867-121">Adding Clever from the gallery</span></span>
2. <span data-ttu-id="c5867-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c5867-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-clever-from-the-gallery"></a><span data-ttu-id="c5867-123">Adicionando o Clever da galeria</span><span class="sxs-lookup"><span data-stu-id="c5867-123">Adding Clever from the gallery</span></span>
<span data-ttu-id="c5867-124">Para configurar a integração do Clever ao Azure AD, você precisará adicionar o Clever da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="c5867-124">To configure the integration of Clever into Azure AD, you need to add Clever from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c5867-125">**Para adicionar o Clever da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="c5867-125">**To add Clever from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c5867-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c5867-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![O botão Azure Active Directory][1]

2. <span data-ttu-id="c5867-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="c5867-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c5867-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="c5867-129">Then go to **All applications**.</span></span>

    ![A folha Aplicativos empresariais][2]
    
3. <span data-ttu-id="c5867-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c5867-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![O botão Novo aplicativo][3]

4. <span data-ttu-id="c5867-133">Na caixa de pesquisa, digite **Clever**, selecione **Clever** no painel de resultados e, em seguida, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c5867-133">In the search box, type **Clever**, select **Clever** from result panel then click **Add** button to add the application.</span></span>

    ![Clever na lista de resultados](./media/active-directory-saas-clever-tutorial/tutorial_clever_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="c5867-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="c5867-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="c5867-136">Nesta seção, você configurará e testará o logon único do Azure AD com o Clever, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="c5867-136">In this section, you configure and test Azure AD single sign-on with Clever based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c5867-137">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Clever é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c5867-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Clever is to a user in Azure AD.</span></span> <span data-ttu-id="c5867-138">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do AD do Azure e o usuário relacionado em Clever.</span><span class="sxs-lookup"><span data-stu-id="c5867-138">In other words, a link relationship between an Azure AD user and the related user in Clever needs to be established.</span></span>

<span data-ttu-id="c5867-139">No Clever, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="c5867-139">In Clever, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="c5867-140">Para configurar e testar o logon único do Azure AD com o Clever, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="c5867-140">To configure and test Azure AD single sign-on with Clever, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c5867-141">**[Configurar o logon único do Azure AD](#configure-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="c5867-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c5867-142">**[Criar um usuário de teste do Azure AD](#create-an-azure-ad-test-user)** – para testar o logon único do Azure AD com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="c5867-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c5867-143">**[Criar um usuário de teste do Clever](#create-a-clever-test-user)** – para ter um equivalente de Brenda Fernandes no Clever que esteja vinculado à representação de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c5867-143">**[Create a Clever test user](#create-a-clever-test-user)** - to have a counterpart of Britta Simon in Clever that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c5867-144">**[Atribuir o usuário de teste do Azure AD](#assign-the-azure-ad-test-user)** – para permitir que Brenda Fernandes use o logon único do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c5867-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c5867-145">**[Teste o logon único](#test-single-sign-on)** – para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="c5867-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="c5867-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="c5867-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="c5867-147">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo Clever.</span><span class="sxs-lookup"><span data-stu-id="c5867-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Clever application.</span></span>

<span data-ttu-id="c5867-148">**Para configurar o logon único do Azure AD com o Clever, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="c5867-148">**To configure Azure AD single sign-on with Clever, perform the following steps:**</span></span>

1. <span data-ttu-id="c5867-149">No portal do Azure, na página de integração do aplicativo **Clever**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="c5867-149">In the Azure portal, on the **Clever** application integration page, click **Single sign-on**.</span></span>

    ![Link Configurar logon único][4]

2. <span data-ttu-id="c5867-151">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="c5867-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-clever-tutorial/tutorial_clever_samlbase.png)

3. <span data-ttu-id="c5867-153">Na seção **URLs e Domínio do Clever**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="c5867-153">On the **Clever Domain and URLs** section, perform the following steps:</span></span>

    ![Informações de logon único em Domínio e URLs do Clever](./media/active-directory-saas-clever-tutorial/tutorial_clever_url.png)

    <span data-ttu-id="c5867-155">a.</span><span class="sxs-lookup"><span data-stu-id="c5867-155">a.</span></span> <span data-ttu-id="c5867-156">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://clever.com/in/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="c5867-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://clever.com/in/<companyname>`</span></span>

    <span data-ttu-id="c5867-157">b.</span><span class="sxs-lookup"><span data-stu-id="c5867-157">b.</span></span> <span data-ttu-id="c5867-158">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://clever.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="c5867-158">In the **Identifier** textbox, type a URL using the following pattern: `https://clever.com/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c5867-159">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="c5867-159">These values are not real.</span></span> <span data-ttu-id="c5867-160">Atualize esses valores com a URL de Entrada e o Identificador reais.</span><span class="sxs-lookup"><span data-stu-id="c5867-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="c5867-161">Contate a [equipe de suporte ao Cliente do Clever](https://clever.com/about/contact/) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="c5867-161">Contact [Clever Client support team](https://clever.com/about/contact/) to get these values.</span></span>

4. <span data-ttu-id="c5867-162">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="c5867-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![O link de download do Certificado](./media/active-directory-saas-clever-tutorial/tutorial_clever_certificate.png)

5. <span data-ttu-id="c5867-164">O aplicativo Clever espera as declarações do SAML em um formato específico, o que exige que você adicione mapeamentos de atributo personalizados de acordo com a sua configuração de **Atributos do Token SAML** .</span><span class="sxs-lookup"><span data-stu-id="c5867-164">The Clever application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your **SAML Token Attributes** configuration.</span></span>

    <span data-ttu-id="c5867-165">A captura de tela a seguir mostra um exemplo disso.</span><span class="sxs-lookup"><span data-stu-id="c5867-165">The following screenshot shows an example for this.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-clever-tutorial/tutorial_clever_07.png) 

6. <span data-ttu-id="c5867-167">Na seção **Atributos do usuário**, na caixa de diálogo **Logon único**, configure o atributo do token SAML na imagem acima e siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="c5867-167">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>
    
    | <span data-ttu-id="c5867-168">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="c5867-168">Attribute Name</span></span>  | <span data-ttu-id="c5867-169">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="c5867-169">Attribute Value</span></span> |
    | --------------- | -------------------- |    
    | <span data-ttu-id="c5867-170">clever.student.credentials.district\_nome de usuário</span><span class="sxs-lookup"><span data-stu-id="c5867-170">clever.student.credentials.district\_username</span></span>  | <span data-ttu-id="c5867-171">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="c5867-171">user.userprincipalname</span></span> |
    | <span data-ttu-id="c5867-172">Firstname</span><span class="sxs-lookup"><span data-stu-id="c5867-172">Firstname</span></span>  | <span data-ttu-id="c5867-173">user.givenname</span><span class="sxs-lookup"><span data-stu-id="c5867-173">user.givenname</span></span> |
    | <span data-ttu-id="c5867-174">Sobrenome</span><span class="sxs-lookup"><span data-stu-id="c5867-174">Lastname</span></span>  | <span data-ttu-id="c5867-175">user.surname</span><span class="sxs-lookup"><span data-stu-id="c5867-175">user.surname</span></span> |    

    <span data-ttu-id="c5867-176">a.</span><span class="sxs-lookup"><span data-stu-id="c5867-176">a.</span></span> <span data-ttu-id="c5867-177">Clique em **Adicionar atributo** para abrir o diálogo **Adicionar Atributo**.</span><span class="sxs-lookup"><span data-stu-id="c5867-177">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-clever-tutorial/tutorial_attribute_04.png)
    
    ![Configurar Logon Único](./media/active-directory-saas-clever-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="c5867-180">b.</span><span class="sxs-lookup"><span data-stu-id="c5867-180">b.</span></span> <span data-ttu-id="c5867-181">Na caixa de texto **Nome** , digite o nome do atributo mostrado para essa linha.</span><span class="sxs-lookup"><span data-stu-id="c5867-181">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="c5867-182">c.</span><span class="sxs-lookup"><span data-stu-id="c5867-182">c.</span></span> <span data-ttu-id="c5867-183">Na lista **Valor**, digite o valor do atributo mostrado para essa linha.</span><span class="sxs-lookup"><span data-stu-id="c5867-183">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="c5867-184">d.</span><span class="sxs-lookup"><span data-stu-id="c5867-184">d.</span></span> <span data-ttu-id="c5867-185">Deixe a caixa de texto **Namespace** em branco.</span><span class="sxs-lookup"><span data-stu-id="c5867-185">Leave the **Namespace** textbox blank.</span></span>
    
    <span data-ttu-id="c5867-186">d.</span><span class="sxs-lookup"><span data-stu-id="c5867-186">d.</span></span> <span data-ttu-id="c5867-187">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="c5867-187">Click **Ok**.</span></span>     

5. <span data-ttu-id="c5867-188">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="c5867-188">Click **Save** button.</span></span>

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-clever-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="c5867-190">Para gerar a URL de **Metadados**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="c5867-190">To generate the **Metadata** url, perform the following steps:</span></span>

    <span data-ttu-id="c5867-191">a.</span><span class="sxs-lookup"><span data-stu-id="c5867-191">a.</span></span> <span data-ttu-id="c5867-192">Clique em **Registros do aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="c5867-192">Click **App registrations**.</span></span>
    
    ![Configurar Logon Único](./media/active-directory-saas-clever-tutorial/tutorial_clever_appregistrations.png)
   
    <span data-ttu-id="c5867-194">b.</span><span class="sxs-lookup"><span data-stu-id="c5867-194">b.</span></span> <span data-ttu-id="c5867-195">Clique em **Pontos de extremidade** para abrir a caixa de diálogo **Pontos de extremidade**.</span><span class="sxs-lookup"><span data-stu-id="c5867-195">Click **Endpoints** to open **Endpoints** dialog box.</span></span>  
    
    ![Configurar Logon Único](./media/active-directory-saas-clever-tutorial/tutorial_clever_endpointicon.png)

    <span data-ttu-id="c5867-197">c.</span><span class="sxs-lookup"><span data-stu-id="c5867-197">c.</span></span> <span data-ttu-id="c5867-198">Clique no botão copiar para copiar a URL **DOCUMENTO DE METADADOS DE FEDERAÇÃO** e cole-a no bloco de notas.</span><span class="sxs-lookup"><span data-stu-id="c5867-198">Click the copy button to copy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Configurar Logon Único](./media/active-directory-saas-clever-tutorial/tutorial_clever_endpoint.png)
     
    <span data-ttu-id="c5867-200">d.</span><span class="sxs-lookup"><span data-stu-id="c5867-200">d.</span></span> <span data-ttu-id="c5867-201">Agora, acesse a página de propriedades do **Clever** e copie a **ID do Aplicativo** usando o botão **Copiar** e cole-a no bloco de notas.</span><span class="sxs-lookup"><span data-stu-id="c5867-201">Now go to the property page of **Clever** and copy the **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-clever-tutorial/tutorial_clever_appid.png)

    <span data-ttu-id="c5867-203">e.</span><span class="sxs-lookup"><span data-stu-id="c5867-203">e.</span></span> <span data-ttu-id="c5867-204">Gere a **URL de Metadados** usando o padrão a seguir: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span><span class="sxs-lookup"><span data-stu-id="c5867-204">Generate the **Metadata URL** using the following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span></span>   

9. <span data-ttu-id="c5867-205">Em outra janela do navegador da Web, faça logon em seu site de empresa do Clever como um administrador.</span><span class="sxs-lookup"><span data-stu-id="c5867-205">In a different web browser window, log in to your Clever company site as an administrator.</span></span>

10. <span data-ttu-id="c5867-206">Na barra de ferramentas, clique em **Logon Instantâneo**.</span><span class="sxs-lookup"><span data-stu-id="c5867-206">In the toolbar, click **Instant Login**.</span></span>

    <span data-ttu-id="c5867-207">![Logon Instantâneo](./media/active-directory-saas-clever-tutorial/ic798984.png "Logon Instantâneo")</span><span class="sxs-lookup"><span data-stu-id="c5867-207">![Instant Login](./media/active-directory-saas-clever-tutorial/ic798984.png "Instant Login")</span></span>

11. <span data-ttu-id="c5867-208">Na página **Logon Instantâneo** , execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="c5867-208">On the **Instant Login** page, perform the following steps:</span></span>
      
      <span data-ttu-id="c5867-209">![Logon Instantâneo](./media/active-directory-saas-clever-tutorial/ic798985.png "Logon Instantâneo")</span><span class="sxs-lookup"><span data-stu-id="c5867-209">![Instant Login](./media/active-directory-saas-clever-tutorial/ic798985.png "Instant Login")</span></span>
      
      <span data-ttu-id="c5867-210">a.</span><span class="sxs-lookup"><span data-stu-id="c5867-210">a.</span></span> <span data-ttu-id="c5867-211">Digite a **URL de Logon**.</span><span class="sxs-lookup"><span data-stu-id="c5867-211">Type the **Login URL**.</span></span>
      
      >[!NOTE]
      ><span data-ttu-id="c5867-212">A **URL de Logon** é um valor personalizado.</span><span class="sxs-lookup"><span data-stu-id="c5867-212">The **Login URL** is a custom value.</span></span> <span data-ttu-id="c5867-213">Contate a [equipe de suporte ao cliente do Clever](https://clever.com/about/contact/) para obter esse valor.</span><span class="sxs-lookup"><span data-stu-id="c5867-213">Contact [Clever Client support team](https://clever.com/about/contact/) to get this value.</span></span>
      
      <span data-ttu-id="c5867-214">b.</span><span class="sxs-lookup"><span data-stu-id="c5867-214">b.</span></span> <span data-ttu-id="c5867-215">Para **Sistema de Identidade**, selecione **ADFS**.</span><span class="sxs-lookup"><span data-stu-id="c5867-215">As **Identity System**, select **ADFS**.</span></span>

      <span data-ttu-id="c5867-216">c.</span><span class="sxs-lookup"><span data-stu-id="c5867-216">c.</span></span> <span data-ttu-id="c5867-217">Tipo de **URL de metadados** na caixa de texto **URL de metadados**.</span><span class="sxs-lookup"><span data-stu-id="c5867-217">Type the **Metadata URL** in the **Metadata URL** textbox.</span></span>
      
      <span data-ttu-id="c5867-218">d.</span><span class="sxs-lookup"><span data-stu-id="c5867-218">d.</span></span> <span data-ttu-id="c5867-219">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="c5867-219">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="c5867-220">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="c5867-220">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c5867-221">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="c5867-221">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c5867-222">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c5867-222">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="c5867-223">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="c5867-223">Create an Azure AD test user</span></span>

<span data-ttu-id="c5867-224">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="c5867-224">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Criar um usuário de teste do Azure AD][100]

<span data-ttu-id="c5867-226">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="c5867-226">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c5867-227">No portal do Azure, no painel esquerdo, clique no botão **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c5867-227">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![O botão Azure Active Directory](./media/active-directory-saas-clever-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="c5867-229">Para exibir a lista de usuários, acesse **Usuários e grupos** e, depois, clique em **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="c5867-229">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Os links “Usuários e grupos” e “Todos os usuários”](./media/active-directory-saas-clever-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="c5867-231">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo **Todos os Usuários**.</span><span class="sxs-lookup"><span data-stu-id="c5867-231">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![O botão Adicionar](./media/active-directory-saas-clever-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="c5867-233">Na caixa de diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="c5867-233">In the **User** dialog box, perform the following steps:</span></span>

    ![A caixa de diálogo Usuário](./media/active-directory-saas-clever-tutorial/create_aaduser_04.png)

    <span data-ttu-id="c5867-235">a.</span><span class="sxs-lookup"><span data-stu-id="c5867-235">a.</span></span> <span data-ttu-id="c5867-236">Na caixa **Nome**, digite **BrendaFernandes**.</span><span class="sxs-lookup"><span data-stu-id="c5867-236">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c5867-237">b.</span><span class="sxs-lookup"><span data-stu-id="c5867-237">b.</span></span> <span data-ttu-id="c5867-238">Na caixa **Nome de usuário**, digite o endereço de email do usuário Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="c5867-238">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="c5867-239">c.</span><span class="sxs-lookup"><span data-stu-id="c5867-239">c.</span></span> <span data-ttu-id="c5867-240">Marque a caixa de seleção **Mostrar Senha** e, em seguida, anote o valor exibido na caixa **Senha**.</span><span class="sxs-lookup"><span data-stu-id="c5867-240">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="c5867-241">d.</span><span class="sxs-lookup"><span data-stu-id="c5867-241">d.</span></span> <span data-ttu-id="c5867-242">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="c5867-242">Click **Create**.</span></span>
 
### <a name="create-a-clever-test-user"></a><span data-ttu-id="c5867-243">Criar um usuário de teste do Clever</span><span class="sxs-lookup"><span data-stu-id="c5867-243">Create a Clever test user</span></span>

<span data-ttu-id="c5867-244">Para permitir que os usuários do Azure AD façam logon no Clever, eles devem ser provisionados no Clever.</span><span class="sxs-lookup"><span data-stu-id="c5867-244">To enable Azure AD users to log in to Clever, they must be provisioned into Clever.</span></span>

<span data-ttu-id="c5867-245">No caso de Clever, trabalhar com [equipe de suporte de Clever Client](https://clever.com/about/contact/) para adicionar os usuários na plataforma Clever.</span><span class="sxs-lookup"><span data-stu-id="c5867-245">In case of Clever, Work with [Clever Client support team](https://clever.com/about/contact/) to add the users in the Clever platform.</span></span> <span data-ttu-id="c5867-246">Os usuários devem ser criados e ativados antes de usar o logon único.</span><span class="sxs-lookup"><span data-stu-id="c5867-246">Users must be created and activated before you use single sign-on.</span></span> 

>[!NOTE]
><span data-ttu-id="c5867-247">É possível usar qualquer outra ferramenta de criação da conta de usuário do Clever ou as APIs fornecidas pelo Clever para provisionar as contas de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c5867-247">You can use any other Clever user account creation tools or APIs provided by Clever to provision Azure AD user accounts.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="c5867-248">Atribuir o usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="c5867-248">Assign the Azure AD test user</span></span>

<span data-ttu-id="c5867-249">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao Clever.</span><span class="sxs-lookup"><span data-stu-id="c5867-249">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Clever.</span></span>

![Atribuir a função de usuário][200] 

<span data-ttu-id="c5867-251">**Para atribuir Britta Simon ao Clever, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="c5867-251">**To assign Britta Simon to Clever, perform the following steps:**</span></span>

1. <span data-ttu-id="c5867-252">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="c5867-252">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="c5867-254">Na lista de aplicativos, selecione **Clever**.</span><span class="sxs-lookup"><span data-stu-id="c5867-254">In the applications list, select **Clever**.</span></span>

    ![O link do Clever na lista de Aplicativos](./media/active-directory-saas-clever-tutorial/tutorial_clever_app.png)  

3. <span data-ttu-id="c5867-256">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="c5867-256">In the menu on the left, click **Users and groups**.</span></span>

    ![O link “Usuários e grupos”][202]

4. <span data-ttu-id="c5867-258">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="c5867-258">Click **Add** button.</span></span> <span data-ttu-id="c5867-259">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c5867-259">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![O painel Adicionar Atribuição][203]

5. <span data-ttu-id="c5867-261">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="c5867-261">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c5867-262">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c5867-262">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c5867-263">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c5867-263">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="c5867-264">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="c5867-264">Test single sign-on</span></span>

<span data-ttu-id="c5867-265">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="c5867-265">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="c5867-266">Ao clicar no bloco de Clever no Painel de Acesso, você deverá ser conectado automaticamente ao aplicativo Clever.</span><span class="sxs-lookup"><span data-stu-id="c5867-266">When you click the Clever tile in the Access Panel, you should get automatically signed-on to your Clever application.</span></span>
<span data-ttu-id="c5867-267">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c5867-267">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="c5867-268">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="c5867-268">Additional resources</span></span>

* [<span data-ttu-id="c5867-269">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="c5867-269">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c5867-270">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c5867-270">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-clever-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-clever-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-clever-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-clever-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-clever-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-clever-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-clever-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-clever-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-clever-tutorial/tutorial_general_203.png

