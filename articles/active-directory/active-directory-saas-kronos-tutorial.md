---
title: "Tutorial: integração do Azure Active Directory ao Kronos | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Kronos."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e28d6191-c375-43c6-b2df-22daa88d9939
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: eb61ec0a7d3e992a285b1af3d4a7fbe1feb8d991
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kronos"></a><span data-ttu-id="5c400-103">Tutorial: integração do Azure Active Directory com o Kronos</span><span class="sxs-lookup"><span data-stu-id="5c400-103">Tutorial: Azure Active Directory integration with Kronos</span></span>

<span data-ttu-id="5c400-104">Neste tutorial, você aprenderá a integrar o Kronos ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="5c400-104">In this tutorial, you learn how to integrate Kronos with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5c400-105">A integração do Kronos ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="5c400-105">Integrating Kronos with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="5c400-106">Você pode controlar no Azure AD quem tem acesso ao Kronos</span><span class="sxs-lookup"><span data-stu-id="5c400-106">You can control in Azure AD who has access to Kronos</span></span>
- <span data-ttu-id="5c400-107">Você pode permitir que usuários façam logon automaticamente no Kronos (logon único) com as respectivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="5c400-107">You can enable your users to automatically get signed-on to Kronos (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5c400-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="5c400-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="5c400-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5c400-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5c400-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="5c400-110">Prerequisites</span></span>

<span data-ttu-id="5c400-111">Para configurar a integração do Azure AD ao Kronos, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="5c400-111">To configure Azure AD integration with Kronos, you need the following items:</span></span>

- <span data-ttu-id="5c400-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="5c400-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5c400-113">Uma assinatura habilitada para SSO do **Kronos Workforce Central**</span><span class="sxs-lookup"><span data-stu-id="5c400-113">A **Kronos Workforce Central** SSO enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5c400-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="5c400-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5c400-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="5c400-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5c400-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="5c400-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5c400-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5c400-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5c400-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="5c400-118">Scenario description</span></span>
<span data-ttu-id="5c400-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="5c400-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5c400-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="5c400-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5c400-121">Adicionando o Kronos da galeria</span><span class="sxs-lookup"><span data-stu-id="5c400-121">Adding Kronos from the gallery</span></span>
2. <span data-ttu-id="5c400-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="5c400-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kronos-from-the-gallery"></a><span data-ttu-id="5c400-123">Adicionando o Kronos da galeria</span><span class="sxs-lookup"><span data-stu-id="5c400-123">Adding Kronos from the gallery</span></span>
<span data-ttu-id="5c400-124">Para configurar a integração do Kronos ao Azure AD, você precisará adicioná-lo da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="5c400-124">To configure the integration of Kronos into Azure AD, you need to add Kronos from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="5c400-125">**Para adicionar o Kronos da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="5c400-125">**To add Kronos from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="5c400-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5c400-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5c400-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="5c400-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="5c400-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="5c400-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="5c400-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5c400-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="5c400-133">Na caixa de pesquisa, digite **Kronos**.</span><span class="sxs-lookup"><span data-stu-id="5c400-133">In the search box, type **Kronos**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_search.png)

5. <span data-ttu-id="5c400-135">No painel de resultados, selecione **Kronos** e, em seguida, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5c400-135">In the results panel, select **Kronos**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5c400-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="5c400-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5c400-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Kronos, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="5c400-138">In this section, you configure and test Azure AD single sign-on with Kronos based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="5c400-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Kronos é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5c400-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Kronos is to a user in Azure AD.</span></span> <span data-ttu-id="5c400-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Kronos.</span><span class="sxs-lookup"><span data-stu-id="5c400-140">In other words, a link relationship between an Azure AD user and the related user in Kronos needs to be established.</span></span>

<span data-ttu-id="5c400-141">No Kronos, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="5c400-141">In Kronos, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="5c400-142">Para configurar e testar o logon único do Azure AD com o Kronos, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="5c400-142">To configure and test Azure AD single sign-on with Kronos, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5c400-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="5c400-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="5c400-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="5c400-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5c400-145">**[Criação de um usuário de teste do Kronos](#creating-a-kronos-test-user)** – para ter um equivalente de Brenda Fernandes no Kronos que esteja vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5c400-145">**[Creating a Kronos test user](#creating-a-kronos-test-user)** - to have a counterpart of Britta Simon in Kronos that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="5c400-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="5c400-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5c400-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="5c400-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5c400-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="5c400-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5c400-149">Nesta seção, você habilitará o logon único do Azure AD no portal do Azure e configurará o logon único em seu aplicativo Kronos.</span><span class="sxs-lookup"><span data-stu-id="5c400-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Kronos application.</span></span>

<span data-ttu-id="5c400-150">**Para configurar o logon único do Azure AD com o Kronos, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="5c400-150">**To configure Azure AD single sign-on with Kronos, perform the following steps:**</span></span>

1. <span data-ttu-id="5c400-151">No portal do Azure, na página de integração de aplicativos do **Kronos**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="5c400-151">In the Azure portal, on the **Kronos** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="5c400-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="5c400-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_samlbase.png)

3. <span data-ttu-id="5c400-155">Na seção **URLs e Domínio do Kronos**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="5c400-155">On the **Kronos Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_url.png)

    <span data-ttu-id="5c400-157">a.</span><span class="sxs-lookup"><span data-stu-id="5c400-157">a.</span></span> <span data-ttu-id="5c400-158">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<company name>.kronos.net/`</span><span class="sxs-lookup"><span data-stu-id="5c400-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<company name>.kronos.net/`</span></span>

    <span data-ttu-id="5c400-159">b.</span><span class="sxs-lookup"><span data-stu-id="5c400-159">b.</span></span> <span data-ttu-id="5c400-160">Na caixa de texto **URL de resposta**, digite uma URL no seguinte padrão: `https://<company name>.kronos.net/wfc/navigator/logonWithUID`</span><span class="sxs-lookup"><span data-stu-id="5c400-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.kronos.net/wfc/navigator/logonWithUID`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5c400-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="5c400-161">These values are not real.</span></span> <span data-ttu-id="5c400-162">Atualize esses valores com o Identificador e a URL de Resposta reais.</span><span class="sxs-lookup"><span data-stu-id="5c400-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="5c400-163">Entre em contato com a [equipe de suporte do Kronos](https://www.kronos.in/contact/en-in/form) para obter valores.</span><span class="sxs-lookup"><span data-stu-id="5c400-163">Contact [Kronos support team](https://www.kronos.in/contact/en-in/form) to get these values.</span></span>
 
4. <span data-ttu-id="5c400-164">O aplicativo Kronos espera que as declarações SAML estejam em um formato específico.</span><span class="sxs-lookup"><span data-stu-id="5c400-164">Your Kronos application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="5c400-165">Trabalhe com a [equipe de suporte do Kronos](https://www.kronos.in/contact/en-in/form) primeiro para verificar o identificador de usuário correto que será mapeado no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5c400-165">Work with [Kronos support team](https://www.kronos.in/contact/en-in/form) first to identify the correct user identifier, which is mapped into the application.</span></span> <span data-ttu-id="5c400-166">Também siga as diretrizes sobre o atributo que deseja usar neste mapeamento.</span><span class="sxs-lookup"><span data-stu-id="5c400-166">Also please take the guidance about the attribute, which they want to use for this mapping.</span></span>
 
     <span data-ttu-id="5c400-167">A Microsoft recomenda usar o atributo **"NameIdentifier"** como identificador de usuário.</span><span class="sxs-lookup"><span data-stu-id="5c400-167">Microsoft recommends using the **"NameIdentifier"** attribute as user identifier.</span></span> <span data-ttu-id="5c400-168">Você pode gerenciar os valores desses atributos da seção **“Atributos de Usuário”** na página de integração do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5c400-168">You can manage the values of these attributes from the **"User Attributes"** section on application integration page.</span></span>
     
     <span data-ttu-id="5c400-169">A captura de tela a seguir mostra um exemplo disso.</span><span class="sxs-lookup"><span data-stu-id="5c400-169">The following screenshot shows an example for this.</span></span> <span data-ttu-id="5c400-170">Aqui nós mapeamos o **Identificador de Usuário (nameid)** com a função **ExtractMailPrefix()** função de **user.userprincipalname**.</span><span class="sxs-lookup"><span data-stu-id="5c400-170">Here we have mapped the **User Identifier (nameid)** with **ExtractMailPrefix()** function of **user.userprincipalname**.</span></span> <span data-ttu-id="5c400-171">Isso retorna o valor de prefixo de email do usuário que é a ID de usuário único.</span><span class="sxs-lookup"><span data-stu-id="5c400-171">This gives the prefix value of email of the user which is the unique User ID.</span></span> <span data-ttu-id="5c400-172">Isto é enviado para o aplicativo Kronos em cada resposta bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="5c400-172">This is sent to the Kronos application in every successful response.</span></span> 
     
    ![Configurar Logon Único](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_attribute.png)

5. <span data-ttu-id="5c400-174">Na seção **Atributos de Usuário**, na caixa de diálogo **Logon único**:</span><span class="sxs-lookup"><span data-stu-id="5c400-174">In the **User Attributes** section on the **Single sign-on** dialog:</span></span>

    <span data-ttu-id="5c400-175">a.</span><span class="sxs-lookup"><span data-stu-id="5c400-175">a.</span></span> <span data-ttu-id="5c400-176">Na lista suspensa Identificador de Usuário, selecione **ExtractMailPrefix**.</span><span class="sxs-lookup"><span data-stu-id="5c400-176">In the User Identifier dropdown list, select **ExtractMailPrefix**.</span></span>

    <span data-ttu-id="5c400-177">b.</span><span class="sxs-lookup"><span data-stu-id="5c400-177">b.</span></span> <span data-ttu-id="5c400-178">Na lista suspensa **Email**, selecione **user.userprincipalname**.</span><span class="sxs-lookup"><span data-stu-id="5c400-178">In the **Mail** dropdown list, select **user.userprincipalname**.</span></span>

6. <span data-ttu-id="5c400-179">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="5c400-179">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_certificate.png) 

7. <span data-ttu-id="5c400-181">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="5c400-181">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-kronos-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="5c400-183">Para configurar o logon único no lado do **Kronos**, é necessário enviar o **XML de metadados** baixado para a [equipe de suporte Kronos](https://www.kronos.in/contact/en-in/form).</span><span class="sxs-lookup"><span data-stu-id="5c400-183">To configure single sign-on on **Kronos** side, you need to send the downloaded **Metadata XML** to [Kronos support team](https://www.kronos.in/contact/en-in/form).</span></span> 

> [!TIP]
> <span data-ttu-id="5c400-184">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="5c400-184">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="5c400-185">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="5c400-185">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="5c400-186">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5c400-186">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5c400-187">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="5c400-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="5c400-188">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="5c400-188">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="5c400-190">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="5c400-190">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5c400-191">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5c400-191">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-kronos-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5c400-193">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="5c400-193">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-kronos-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5c400-195">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5c400-195">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-kronos-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5c400-197">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="5c400-197">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-kronos-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5c400-199">a.</span><span class="sxs-lookup"><span data-stu-id="5c400-199">a.</span></span> <span data-ttu-id="5c400-200">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="5c400-200">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5c400-201">b.</span><span class="sxs-lookup"><span data-stu-id="5c400-201">b.</span></span> <span data-ttu-id="5c400-202">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="5c400-202">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5c400-203">c.</span><span class="sxs-lookup"><span data-stu-id="5c400-203">c.</span></span> <span data-ttu-id="5c400-204">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="5c400-204">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="5c400-205">d.</span><span class="sxs-lookup"><span data-stu-id="5c400-205">d.</span></span> <span data-ttu-id="5c400-206">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="5c400-206">Click **Create**.</span></span>
 
### <a name="creating-a-kronos-test-user"></a><span data-ttu-id="5c400-207">Criar um usuário de teste do Kronos</span><span class="sxs-lookup"><span data-stu-id="5c400-207">Creating a Kronos test user</span></span>

<span data-ttu-id="5c400-208">Nesta seção, você criará um usuário chamado Brenda Fernandes no Kronos.</span><span class="sxs-lookup"><span data-stu-id="5c400-208">In this section, you create a user called Britta Simon in Kronos.</span></span> <span data-ttu-id="5c400-209">O aplicativo Kronos precisa que todos os usuários sejam provisionados no aplicativo antes de fazer o SSO.</span><span class="sxs-lookup"><span data-stu-id="5c400-209">Kronos application needs all the users to be provisioned in the application before doing SSO.</span></span> 

<span data-ttu-id="5c400-210">Trabalhe com a [equipe de suporte do Kronos](https://www.kronos.in/contact/en-in/form) para provisionar todos esses usuários no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5c400-210">Work with the [Kronos support team](https://www.kronos.in/contact/en-in/form) to provision all these users into the application.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="5c400-211">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="5c400-211">Assigning the Azure AD test user</span></span>

<span data-ttu-id="5c400-212">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo a ela acesso ao Kronos.</span><span class="sxs-lookup"><span data-stu-id="5c400-212">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Kronos.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="5c400-214">**Para atribuir Brenda Fernandes ao Kronos, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="5c400-214">**To assign Britta Simon to Kronos, perform the following steps:**</span></span>

1. <span data-ttu-id="5c400-215">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="5c400-215">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="5c400-217">Na lista de aplicativos, escolha **Kronos**.</span><span class="sxs-lookup"><span data-stu-id="5c400-217">In the applications list, select **Kronos**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_app.png) 

3. <span data-ttu-id="5c400-219">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="5c400-219">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="5c400-221">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="5c400-221">Click **Add** button.</span></span> <span data-ttu-id="5c400-222">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5c400-222">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="5c400-224">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="5c400-224">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="5c400-225">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5c400-225">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5c400-226">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5c400-226">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5c400-227">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="5c400-227">Testing single sign-on</span></span>

<span data-ttu-id="5c400-228">Nesta seção, você testará sua configuração de SSO do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="5c400-228">In this section, you test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="5c400-229">Ao clicar no bloco Kronos no Painel de Acesso, você deverá ser conectado automaticamente ao seu aplicativo Kronos.</span><span class="sxs-lookup"><span data-stu-id="5c400-229">When you click the Kronos tile in the Access Panel, you should get automatically signed-on to your Kronos application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5c400-230">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="5c400-230">Additional resources</span></span>

* [<span data-ttu-id="5c400-231">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="5c400-231">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5c400-232">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5c400-232">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_203.png

