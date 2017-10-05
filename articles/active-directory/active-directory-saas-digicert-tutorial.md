---
title: "Tutorial: Integração do Azure Active Directory ao DigiCert | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o DigiCert."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 646f3129-aa67-4875-9073-1d0b6a3173d9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jeedes
ms.openlocfilehash: 2ceb3c0833edcd4ecd875c5e8006961ed7216c66
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-digicert"></a><span data-ttu-id="f0cc0-103">Tutorial: integração do Azure Active Directory com o DigiCert</span><span class="sxs-lookup"><span data-stu-id="f0cc0-103">Tutorial: Azure Active Directory integration with DigiCert</span></span>

<span data-ttu-id="f0cc0-104">Neste tutorial, você aprenderá a integrar o DigiCert ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="f0cc0-104">In this tutorial, you learn how to integrate DigiCert with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f0cc0-105">A integração do DigiCert ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="f0cc0-105">Integrating DigiCert with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f0cc0-106">No Azure AD, é possível controlar quem tem acesso ao DigiCert</span><span class="sxs-lookup"><span data-stu-id="f0cc0-106">You can control in Azure AD who has access to DigiCert</span></span>
- <span data-ttu-id="f0cc0-107">Você pode permitir que seus usuários façam logon automaticamente no DigiCert (Logon Único) com as próprias contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="f0cc0-107">You can enable your users to automatically get signed-on to DigiCert (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f0cc0-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="f0cc0-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="f0cc0-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f0cc0-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f0cc0-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="f0cc0-110">Prerequisites</span></span>

<span data-ttu-id="f0cc0-111">Para configurar a integração do Azure AD ao DigiCert, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="f0cc0-111">To configure Azure AD integration with DigiCert, you need the following items:</span></span>

- <span data-ttu-id="f0cc0-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f0cc0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f0cc0-113">Uma assinatura habilitada para logon único do DigiCert</span><span class="sxs-lookup"><span data-stu-id="f0cc0-113">A DigiCert single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f0cc0-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="f0cc0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f0cc0-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="f0cc0-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f0cc0-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="f0cc0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f0cc0-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f0cc0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f0cc0-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="f0cc0-118">Scenario description</span></span>
<span data-ttu-id="f0cc0-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="f0cc0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f0cc0-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="f0cc0-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f0cc0-121">Adicionando DigiCert da galeria</span><span class="sxs-lookup"><span data-stu-id="f0cc0-121">Adding DigiCert from the gallery</span></span>
2. <span data-ttu-id="f0cc0-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f0cc0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-digicert-from-the-gallery"></a><span data-ttu-id="f0cc0-123">Adicionando DigiCert da galeria</span><span class="sxs-lookup"><span data-stu-id="f0cc0-123">Adding DigiCert from the gallery</span></span>
<span data-ttu-id="f0cc0-124">Para configurar a integração do DigiCert ao Azure AD, você precisará adicionar o DigiCert da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="f0cc0-124">To configure the integration of DigiCert into Azure AD, you need to add DigiCert from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f0cc0-125">**Para adicionar o DigiCert da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="f0cc0-125">**To add DigiCert from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f0cc0-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f0cc0-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f0cc0-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="f0cc0-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f0cc0-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="f0cc0-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="f0cc0-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f0cc0-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="f0cc0-133">Na caixa de pesquisa, digite **DigiCert**.</span><span class="sxs-lookup"><span data-stu-id="f0cc0-133">In the search box, type **DigiCert**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_search.png)

5. <span data-ttu-id="f0cc0-135">No painel de resultados, selecione **DigiCert** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f0cc0-135">In the results panel, select **DigiCert**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f0cc0-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f0cc0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f0cc0-138">Nesta seção, você configurará e testará o logon único do Azure AD com o DigiCert com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="f0cc0-138">In this section, you configure and test Azure AD single sign-on with DigiCert based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="f0cc0-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do DigiCert é equivalente a um usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f0cc0-139">For single sign-on to work, Azure AD needs to know what the counterpart user in DigiCert is to a user in Azure AD.</span></span> <span data-ttu-id="f0cc0-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do DigiCert.</span><span class="sxs-lookup"><span data-stu-id="f0cc0-140">In other words, a link relationship between an Azure AD user and the related user in DigiCert needs to be established.</span></span>

<span data-ttu-id="f0cc0-141">No DigiCert, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="f0cc0-141">In DigiCert, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="f0cc0-142">Para configurar e testar o logon único do Azure AD com o DigiCert, você precisará concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="f0cc0-142">To configure and test Azure AD single sign-on with DigiCert, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f0cc0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="f0cc0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f0cc0-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="f0cc0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f0cc0-145">**[Criação de um usuário de teste do DigiCert](#creating-a-digicert-test-user)** – para ter um equivalente de Brenda Fernandes no DigiCert que esteja vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f0cc0-145">**[Creating a DigiCert test user](#creating-a-digicert-test-user)** - to have a counterpart of Britta Simon in DigiCert that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="f0cc0-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="f0cc0-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f0cc0-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="f0cc0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f0cc0-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="f0cc0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f0cc0-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único em seu aplicativo DigiCert.</span><span class="sxs-lookup"><span data-stu-id="f0cc0-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your DigiCert application.</span></span>

<span data-ttu-id="f0cc0-150">**Para configurar o logon único do Azure AD com o DigiCert, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="f0cc0-150">**To configure Azure AD single sign-on with DigiCert, perform the following steps:**</span></span>

1. <span data-ttu-id="f0cc0-151">No portal do Azure, na página de integração de aplicativos do **DigiCert**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="f0cc0-151">In the Azure portal, on the **DigiCert** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="f0cc0-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="f0cc0-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_samlbase.png)

3. <span data-ttu-id="f0cc0-155">Na seção **URLs e Domínio do DigiCert**, o usuário não precisa executar nenhuma etapa, já que o aplicativo já está pré-integrado ao Azure.</span><span class="sxs-lookup"><span data-stu-id="f0cc0-155">On the **DigiCert Domain and URLs** section, the user does not have to perform any steps as the app is already pre-integrated with Azure.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_url.png)

4. <span data-ttu-id="f0cc0-157">O aplicativo DigiCert espera que as instruções SAML estejam em um formato específico.</span><span class="sxs-lookup"><span data-stu-id="f0cc0-157">DigiCert application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="f0cc0-158">Configure as declarações a seguir para este aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f0cc0-158">Configure the following claims for this application.</span></span> <span data-ttu-id="f0cc0-159">Você pode gerenciar os valores desses atributos da seção "**Atributos de Usuário**" na página de integração do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f0cc0-159">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="f0cc0-160">A captura de tela a seguir mostra um exemplo dessa configuração.</span><span class="sxs-lookup"><span data-stu-id="f0cc0-160">The following screenshot shows an example for this configuration.</span></span> 

    ![Configurar Logon Único](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_attributes.png)
    
5. <span data-ttu-id="f0cc0-162">Na seção **Atributos do Usuário**, na caixa de diálogo **Logon único**, configure o atributo do token SAML como mostra a imagem e execute as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="f0cc0-162">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="f0cc0-163">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="f0cc0-163">Attribute Name</span></span> | <span data-ttu-id="f0cc0-164">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="f0cc0-164">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="f0cc0-165">company</span><span class="sxs-lookup"><span data-stu-id="f0cc0-165">company</span></span> | <span data-ttu-id="f0cc0-166">< companycode ></span><span class="sxs-lookup"><span data-stu-id="f0cc0-166">< companycode ></span></span> |
    | <span data-ttu-id="f0cc0-167">digicertrole</span><span class="sxs-lookup"><span data-stu-id="f0cc0-167">digicertrole</span></span> | <span data-ttu-id="f0cc0-168">CanAccessCertCentral</span><span class="sxs-lookup"><span data-stu-id="f0cc0-168">CanAccessCertCentral</span></span> |

    > [!Note]
    > <span data-ttu-id="f0cc0-169">O valor do atributo **company** não é real.</span><span class="sxs-lookup"><span data-stu-id="f0cc0-169">The value of **company** attribute is not real.</span></span> <span data-ttu-id="f0cc0-170">Atualize esse valor com o código da empresa real.</span><span class="sxs-lookup"><span data-stu-id="f0cc0-170">Update this value with actual company code.</span></span> <span data-ttu-id="f0cc0-171">Para obter o valor do atributo **company**, entre em contato com [a equipe de suporte do DigiCert](mailto:support@digicert.com).</span><span class="sxs-lookup"><span data-stu-id="f0cc0-171">To get the value of **company** attribute contact [DigiCert support team](mailto:support@digicert.com).</span></span>

    <span data-ttu-id="f0cc0-172">a.</span><span class="sxs-lookup"><span data-stu-id="f0cc0-172">a.</span></span> <span data-ttu-id="f0cc0-173">Clique em **Adicionar atributo** para abrir o diálogo **Adicionar Atributo**.</span><span class="sxs-lookup"><span data-stu-id="f0cc0-173">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-digicert-tutorial/tutorial_attribute_04.png)

    ![Configurar Logon Único](./media/active-directory-saas-digicert-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="f0cc0-176">b.</span><span class="sxs-lookup"><span data-stu-id="f0cc0-176">b.</span></span> <span data-ttu-id="f0cc0-177">Na caixa de texto **Nome** , digite o nome do atributo mostrado para essa linha.</span><span class="sxs-lookup"><span data-stu-id="f0cc0-177">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="f0cc0-178">c.</span><span class="sxs-lookup"><span data-stu-id="f0cc0-178">c.</span></span> <span data-ttu-id="f0cc0-179">Na lista **Valor**, digite o valor do atributo mostrado para essa linha.</span><span class="sxs-lookup"><span data-stu-id="f0cc0-179">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="f0cc0-180">d.</span><span class="sxs-lookup"><span data-stu-id="f0cc0-180">d.</span></span> <span data-ttu-id="f0cc0-181">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="f0cc0-181">Click **Ok**.</span></span> 

6. <span data-ttu-id="f0cc0-182">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="f0cc0-182">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_certificate.png) 

7. <span data-ttu-id="f0cc0-184">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="f0cc0-184">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-digicert-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="f0cc0-186">Para configurar o logon único no lado do **DigiCert**, é necessário enviar o **XML de metadados** baixado para a [equipe de suporte do DigiCert](mailto:support@digicert.com).</span><span class="sxs-lookup"><span data-stu-id="f0cc0-186">To configure single sign-on on **DigiCert** side, you need to send the downloaded **Metadata XML** to [DigiCert support team](mailto:support@digicert.com).</span></span> <span data-ttu-id="f0cc0-187">Eles definem essa configuração para ter a conexão de SSO do SAML definida corretamente em ambos os lados.</span><span class="sxs-lookup"><span data-stu-id="f0cc0-187">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="f0cc0-188">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="f0cc0-188">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f0cc0-189">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="f0cc0-189">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f0cc0-190">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f0cc0-190">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f0cc0-191">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f0cc0-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="f0cc0-192">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="f0cc0-192">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="f0cc0-194">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="f0cc0-194">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f0cc0-195">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f0cc0-195">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-digicert-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f0cc0-197">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="f0cc0-197">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-digicert-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f0cc0-199">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f0cc0-199">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-digicert-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f0cc0-201">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="f0cc0-201">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-digicert-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f0cc0-203">a.</span><span class="sxs-lookup"><span data-stu-id="f0cc0-203">a.</span></span> <span data-ttu-id="f0cc0-204">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="f0cc0-204">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f0cc0-205">b.</span><span class="sxs-lookup"><span data-stu-id="f0cc0-205">b.</span></span> <span data-ttu-id="f0cc0-206">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="f0cc0-206">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f0cc0-207">c.</span><span class="sxs-lookup"><span data-stu-id="f0cc0-207">c.</span></span> <span data-ttu-id="f0cc0-208">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="f0cc0-208">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="f0cc0-209">d.</span><span class="sxs-lookup"><span data-stu-id="f0cc0-209">d.</span></span> <span data-ttu-id="f0cc0-210">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="f0cc0-210">Click **Create**.</span></span>
 
### <a name="creating-a-digicert-test-user"></a><span data-ttu-id="f0cc0-211">Como criar um usuário de teste DigiCert</span><span class="sxs-lookup"><span data-stu-id="f0cc0-211">Creating a DigiCert test user</span></span>

<span data-ttu-id="f0cc0-212">Nesta seção, você criará um usuário chamado Brenda Fernandes no DigiCert.</span><span class="sxs-lookup"><span data-stu-id="f0cc0-212">In this section, you create a user called Britta Simon in DigiCert.</span></span> <span data-ttu-id="f0cc0-213">Trabalhe com [a equipe de suporte do DigiCert](mailto:support@digicert.com) para adicionar os usuários ao DigiCert.</span><span class="sxs-lookup"><span data-stu-id="f0cc0-213">Please work with [DigiCert support team](mailto:support@digicert.com) to add the users in DigiCert.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="f0cc0-214">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f0cc0-214">Assigning the Azure AD test user</span></span>

<span data-ttu-id="f0cc0-215">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo acesso ao DigiCert.</span><span class="sxs-lookup"><span data-stu-id="f0cc0-215">In this section, you enable Britta Simon to use Azure single sign-on by granting access to DigiCert.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="f0cc0-217">**Para atribuir Brenda Fernandes ao DigiCert, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="f0cc0-217">**To assign Britta Simon to DigiCert, perform the following steps:**</span></span>

1. <span data-ttu-id="f0cc0-218">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="f0cc0-218">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="f0cc0-220">Na lista de aplicativos, selecione **DigiCert**.</span><span class="sxs-lookup"><span data-stu-id="f0cc0-220">In the applications list, select **DigiCert**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_app.png) 

3. <span data-ttu-id="f0cc0-222">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="f0cc0-222">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="f0cc0-224">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="f0cc0-224">Click **Add** button.</span></span> <span data-ttu-id="f0cc0-225">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f0cc0-225">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="f0cc0-227">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="f0cc0-227">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f0cc0-228">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f0cc0-228">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f0cc0-229">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f0cc0-229">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f0cc0-230">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="f0cc0-230">Testing single sign-on</span></span>

<span data-ttu-id="f0cc0-231">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="f0cc0-231">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="f0cc0-232">Quando você clicar no bloco DigiCert no Painel de Acesso, deverá fazer logon automaticamente no seu aplicativo DeigiCert.</span><span class="sxs-lookup"><span data-stu-id="f0cc0-232">When you click the DigiCert tile in the Access Panel, you should get automatically signed-on to your DeigiCert application.</span></span>
<span data-ttu-id="f0cc0-233">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f0cc0-233">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="f0cc0-234">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="f0cc0-234">Additional resources</span></span>

* [<span data-ttu-id="f0cc0-235">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="f0cc0-235">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f0cc0-236">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f0cc0-236">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_203.png

