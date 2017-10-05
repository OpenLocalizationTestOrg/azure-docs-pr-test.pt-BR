---
title: "Tutorial: Integração do Azure Active Directory ao 123ContactForm | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o 123ContactForm."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5211910a-ab96-4709-959a-524c4d57c43e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 3a99f0841c3e0d973168991f5dbee40e54c1d054
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-123contactform"></a><span data-ttu-id="8d534-103">Tutorial: Integração do Azure Active Directory ao 123ContactForm</span><span class="sxs-lookup"><span data-stu-id="8d534-103">Tutorial: Azure Active Directory integration with 123ContactForm</span></span>

<span data-ttu-id="8d534-104">Neste tutorial, você aprende a integrar o 123ContactForm ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="8d534-104">In this tutorial, you learn how to integrate 123ContactForm with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8d534-105">A integração do 123ContactForm ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="8d534-105">Integrating 123ContactForm with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="8d534-106">No Azure AD, é possível controlar quem tem acesso ao 123ContactForm</span><span class="sxs-lookup"><span data-stu-id="8d534-106">You can control in Azure AD who has access to 123ContactForm</span></span>
- <span data-ttu-id="8d534-107">É possível permitir que os usuários se conectem automaticamente ao 123ContactForm (Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="8d534-107">You can enable your users to automatically get signed-on to 123ContactForm (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8d534-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="8d534-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="8d534-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8d534-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8d534-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="8d534-110">Prerequisites</span></span>

<span data-ttu-id="8d534-111">Para configurar a integração do Azure AD ao 123ContactForm, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="8d534-111">To configure Azure AD integration with 123ContactForm, you need the following items:</span></span>

- <span data-ttu-id="8d534-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8d534-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8d534-113">Uma assinatura habilitada para logon único do 123ContactForm</span><span class="sxs-lookup"><span data-stu-id="8d534-113">A 123ContactForm single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8d534-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="8d534-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8d534-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="8d534-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8d534-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="8d534-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8d534-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8d534-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8d534-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="8d534-118">Scenario description</span></span>
<span data-ttu-id="8d534-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="8d534-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8d534-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="8d534-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8d534-121">Adicionando o 123ContactForm por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="8d534-121">Adding 123ContactForm from the gallery</span></span>
2. <span data-ttu-id="8d534-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8d534-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-123contactform-from-the-gallery"></a><span data-ttu-id="8d534-123">Adicionando o 123ContactForm por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="8d534-123">Adding 123ContactForm from the gallery</span></span>
<span data-ttu-id="8d534-124">Para configurar a integração do 123ContactForm ao Azure AD, você precisa adicionar o 123ContactForm à lista de aplicativos SaaS gerenciados por meio da galeria.</span><span class="sxs-lookup"><span data-stu-id="8d534-124">To configure the integration of 123ContactForm into Azure AD, you need to add 123ContactForm from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8d534-125">**Para adicionar o 123ContactForm por meio da galeria, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="8d534-125">**To add 123ContactForm from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8d534-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8d534-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8d534-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="8d534-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="8d534-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="8d534-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="8d534-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8d534-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="8d534-133">Na caixa de pesquisa, digite **123ContactForm**.</span><span class="sxs-lookup"><span data-stu-id="8d534-133">In the search box, type **123ContactForm**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_search.png)

5. <span data-ttu-id="8d534-135">No painel de resultados, selecione **123ContactForm** e, depois, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8d534-135">In the results panel, select **123ContactForm**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8d534-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8d534-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8d534-138">Nesta seção, você configura e testa o logon único do Azure AD com o 123ContactForm, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="8d534-138">In this section, you configure and test Azure AD single sign-on with 123ContactForm based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="8d534-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do 123ContactForm é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8d534-139">For single sign-on to work, Azure AD needs to know what the counterpart user in 123ContactForm is to a user in Azure AD.</span></span> <span data-ttu-id="8d534-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do 123ContactForm.</span><span class="sxs-lookup"><span data-stu-id="8d534-140">In other words, a link relationship between an Azure AD user and the related user in 123ContactForm needs to be established.</span></span>

<span data-ttu-id="8d534-141">No 123ContactForm, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="8d534-141">In 123ContactForm, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="8d534-142">Para configurar e testar o logon único do Azure AD com o 123ContactForm, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="8d534-142">To configure and test Azure AD single sign-on with 123ContactForm, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8d534-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="8d534-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="8d534-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="8d534-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8d534-145">**[Criando um usuário de teste do 123ContactForm](#creating-a-123contactform-test-user)** – para ter um equivalente de Brenda Fernandes no 123ContactForm que esteja vinculado à representação de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8d534-145">**[Creating a 123ContactForm test user](#creating-a-123contactform-test-user)** - to have a counterpart of Britta Simon in 123ContactForm that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="8d534-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="8d534-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8d534-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="8d534-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8d534-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="8d534-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8d534-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo 123ContactForm.</span><span class="sxs-lookup"><span data-stu-id="8d534-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your 123ContactForm application.</span></span>

<span data-ttu-id="8d534-150">**Para configurar o logon único do Azure AD com o 123ContactForm, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="8d534-150">**To configure Azure AD single sign-on with 123ContactForm, perform the following steps:**</span></span>

1. <span data-ttu-id="8d534-151">No portal do Azure, na página de integração do aplicativo do **123ContactForm**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="8d534-151">In the Azure portal, on the **123ContactForm** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="8d534-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="8d534-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_samlbase.png)

3. <span data-ttu-id="8d534-155">Na seção **Domínio e URLs do 123ContactForm**, se desejar configurar o aplicativo no **modo iniciado pelo IDP**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="8d534-155">On the **123ContactForm Domain and URLs** section, If you wish to configure the application in **IDP initiated mode**, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-123contactform-tutorial/url1.png)

    <span data-ttu-id="8d534-157">a.</span><span class="sxs-lookup"><span data-stu-id="8d534-157">a.</span></span> <span data-ttu-id="8d534-158">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://www.123contactform.com/saml/azure_ad/<tenant_id>/metadata`</span><span class="sxs-lookup"><span data-stu-id="8d534-158">In the **Identifier** textbox, type a URL using the following pattern: `https://www.123contactform.com/saml/azure_ad/<tenant_id>/metadata`</span></span>

    <span data-ttu-id="8d534-159">b.</span><span class="sxs-lookup"><span data-stu-id="8d534-159">b.</span></span> <span data-ttu-id="8d534-160">Na caixa de texto **URL de resposta**, digite uma URL no seguinte padrão: `https://www.123contactform.com/saml/azure_ad/<tenant_id>/acs`</span><span class="sxs-lookup"><span data-stu-id="8d534-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://www.123contactform.com/saml/azure_ad/<tenant_id>/acs`</span></span>

4. <span data-ttu-id="8d534-161">Se desejar configurar o aplicativo no **modo iniciado pelo SP**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="8d534-161">If you wish to configure the application in **SP initiated mode**, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-123contactform-tutorial/url2.png)

    <span data-ttu-id="8d534-163">a.</span><span class="sxs-lookup"><span data-stu-id="8d534-163">a.</span></span> <span data-ttu-id="8d534-164">Clique na opção **Mostrar configurações de URL avançadas**</span><span class="sxs-lookup"><span data-stu-id="8d534-164">Click the **Show advanced URL settings** option</span></span>

    <span data-ttu-id="8d534-165">b.</span><span class="sxs-lookup"><span data-stu-id="8d534-165">b.</span></span> <span data-ttu-id="8d534-166">Na caixa de texto **URL de Logon**, digite uma URL como: `https://www.123contactform.com/saml/azure_ad/<tenant_id>/sso`</span><span class="sxs-lookup"><span data-stu-id="8d534-166">In the **Sign On URL** textbox, type a URL as: `https://www.123contactform.com/saml/azure_ad/<tenant_id>/sso`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8d534-167">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="8d534-167">These values are not real.</span></span> <span data-ttu-id="8d534-168">Você precisará atualizar esse valor com o Identificador e as URLs reais que são explicadas posteriormente no tutorial.</span><span class="sxs-lookup"><span data-stu-id="8d534-168">You'll need to update these value from actual URLs and Identifier which is explained later in the tutorial.</span></span>
    
5. <span data-ttu-id="8d534-169">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="8d534-169">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_certificate.png) 

6. <span data-ttu-id="8d534-171">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="8d534-171">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-123contactform-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="8d534-173">Para configurar o logon único no lado do **123ContactForm**, acesse [https://www.123contactform.com/form-2709121/](https://www.123contactform.com/form-2709121/) e realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="8d534-173">To configure single sign-on on **123ContactForm** side, go to [https://www.123contactform.com/form-2709121/](https://www.123contactform.com/form-2709121/) and perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-123contactform-tutorial/submit.png) 

    <span data-ttu-id="8d534-175">a.</span><span class="sxs-lookup"><span data-stu-id="8d534-175">a.</span></span> <span data-ttu-id="8d534-176">Na caixa de texto **Email**, digite o email do usuário, ou seja,</span><span class="sxs-lookup"><span data-stu-id="8d534-176">In the **Email** textbox, type the email of the user i.e</span></span> <span data-ttu-id="8d534-177">**BrittaSimon@Contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="8d534-177">**BrittaSimon@Contoso.com**.</span></span>

    <span data-ttu-id="8d534-178">b.</span><span class="sxs-lookup"><span data-stu-id="8d534-178">b.</span></span> <span data-ttu-id="8d534-179">Clique em **Carregar** e procure o arquivo XML de Metadados baixado no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="8d534-179">Click **Upload** and browse the Metadata XML file, which you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="8d534-180">c.</span><span class="sxs-lookup"><span data-stu-id="8d534-180">c.</span></span> <span data-ttu-id="8d534-181">Clique em **ENVIAR FORMULÁRIO**.</span><span class="sxs-lookup"><span data-stu-id="8d534-181">Click **SUBMIT FORM**.</span></span>

8. <span data-ttu-id="8d534-182">Em **Microsoft Azure AD – Logon único – Definir Configurações do Aplicativo**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="8d534-182">On the **Microsoft Azure AD - Single sign-on - Configure App Settings** perform the following steps:</span></span>
    
    ![Configurar Logon Único](./media/active-directory-saas-123contactform-tutorial/url3.png)

    <span data-ttu-id="8d534-184">a.</span><span class="sxs-lookup"><span data-stu-id="8d534-184">a.</span></span> <span data-ttu-id="8d534-185">Se desejar configurar o aplicativo no **modo iniciado pelo IDP**, copie o valor do **IDENTIFICADOR** da instância e cole-o na caixa de texto **Identificador** da seção **Domínio e URLs do 123ContactForm** no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="8d534-185">If you wish to configure the application in **IDP initiated mode**, copy the **IDENTIFIER** value for your instance and paste it in **Identifier** textbox in **123ContactForm Domain and URLs** section on Azure portal.</span></span>
    
    <span data-ttu-id="8d534-186">b.</span><span class="sxs-lookup"><span data-stu-id="8d534-186">b.</span></span> <span data-ttu-id="8d534-187">Se desejar configurar o aplicativo no **modo iniciado pelo IDP**, copie o valor da **URL DE RESPOSTA** da instância e cole-o na caixa de texto **URL de Resposta** da seção **Domínio e URLs do 123ContactForm** no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="8d534-187">If you wish to configure the application in **IDP initiated mode**, copy the **REPLY URL** value for your instance and paste it in **Reply URL** textbox in **123ContactForm Domain and URLs** section on Azure portal.</span></span>

    <span data-ttu-id="8d534-188">c.</span><span class="sxs-lookup"><span data-stu-id="8d534-188">c.</span></span> <span data-ttu-id="8d534-189">Se desejar configurar o aplicativo no **modo iniciado pelo SP**, copie o valor da **URL DE LOGON** da instância e cole-o na caixa de texto **URL de Logon** da seção **Domínio e URLs do 123ContactForm** no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="8d534-189">If you wish to configure the application in **SP initiated mode**, copy the **SIGN ON URL** value for your instance and paste it in **Sign On URL** textbox in **123ContactForm Domain and URLs** section on Azure portal.</span></span>

> [!TIP]
> <span data-ttu-id="8d534-190">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="8d534-190">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="8d534-191">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="8d534-191">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="8d534-192">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8d534-192">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8d534-193">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8d534-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="8d534-194">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="8d534-194">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="8d534-196">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="8d534-196">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8d534-197">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8d534-197">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-123contactform-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8d534-199">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="8d534-199">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-123contactform-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8d534-201">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8d534-201">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-123contactform-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8d534-203">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="8d534-203">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-123contactform-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8d534-205">a.</span><span class="sxs-lookup"><span data-stu-id="8d534-205">a.</span></span> <span data-ttu-id="8d534-206">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="8d534-206">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8d534-207">b.</span><span class="sxs-lookup"><span data-stu-id="8d534-207">b.</span></span> <span data-ttu-id="8d534-208">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="8d534-208">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8d534-209">c.</span><span class="sxs-lookup"><span data-stu-id="8d534-209">c.</span></span> <span data-ttu-id="8d534-210">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="8d534-210">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="8d534-211">d.</span><span class="sxs-lookup"><span data-stu-id="8d534-211">d.</span></span> <span data-ttu-id="8d534-212">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="8d534-212">Click **Create**.</span></span>
 
### <a name="creating-a-123contactform-test-user"></a><span data-ttu-id="8d534-213">Criando um usuário de teste do 123ContactForm</span><span class="sxs-lookup"><span data-stu-id="8d534-213">Creating a 123ContactForm test user</span></span>

<span data-ttu-id="8d534-214">O aplicativo dá suporte ao provisionamento de usuário just-in-time e, após a autenticação, os usuários serão automaticamente criados no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8d534-214">Application supports Just in time user provisioning and after authentication users will be created in the application automatically.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="8d534-215">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8d534-215">Assigning the Azure AD test user</span></span>

<span data-ttu-id="8d534-216">Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo acesso ao 123ContactForm.</span><span class="sxs-lookup"><span data-stu-id="8d534-216">In this section, you enable Britta Simon to use Azure single sign-on by granting access to 123ContactForm.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="8d534-218">**Para atribuir Brenda Fernandes ao 123ContactForm, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="8d534-218">**To assign Britta Simon to 123ContactForm, perform the following steps:**</span></span>

1. <span data-ttu-id="8d534-219">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="8d534-219">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="8d534-221">Na lista de aplicativos, selecione **123ContactForm**.</span><span class="sxs-lookup"><span data-stu-id="8d534-221">In the applications list, select **123ContactForm**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_app.png) 

3. <span data-ttu-id="8d534-223">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="8d534-223">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="8d534-225">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="8d534-225">Click **Add** button.</span></span> <span data-ttu-id="8d534-226">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8d534-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="8d534-228">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="8d534-228">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="8d534-229">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8d534-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8d534-230">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8d534-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8d534-231">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="8d534-231">Testing single sign-on</span></span>

<span data-ttu-id="8d534-232">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="8d534-232">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="8d534-233">Quando você clicar no bloco 123ContactForm no Painel de Acesso, deverá ser automaticamente conectado ao aplicativo 123ContactForm.</span><span class="sxs-lookup"><span data-stu-id="8d534-233">When you click the 123ContactForm tile in the Access Panel, you should get automatically signed-on to your 123ContactForm application.</span></span>
<span data-ttu-id="8d534-234">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8d534-234">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8d534-235">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="8d534-235">Additional resources</span></span>

* [<span data-ttu-id="8d534-236">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="8d534-236">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8d534-237">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8d534-237">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_203.png

