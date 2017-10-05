---
title: "Tutorial: Integração do Azure Active Directory com o Neota Logic Studio | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Neota Logic Studio."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 842605e6-a91d-42cc-a0bb-e23e67173ae2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/03/2017
ms.author: jeedes
ms.openlocfilehash: 99018277392cab44a6b579ad45b4611739a803d8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-neota-logic-studio"></a><span data-ttu-id="ab035-103">Tutorial: Integração do Azure Active Directory com o Neota Logic Studio</span><span class="sxs-lookup"><span data-stu-id="ab035-103">Tutorial: Azure Active Directory integration with Neota Logic Studio</span></span>

<span data-ttu-id="ab035-104">Neste tutorial, você aprenderá a integrar o Neota Logic Studio ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="ab035-104">In this tutorial, you learn how to integrate Neota Logic Studio with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ab035-105">A integração do Neota Logic Studio ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="ab035-105">Integrating Neota Logic Studio with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ab035-106">No Azure AD, você pode controlar quem tem acesso ao Neota Logic Studio</span><span class="sxs-lookup"><span data-stu-id="ab035-106">You can control in Azure AD who has access to Neota Logic Studio</span></span>
- <span data-ttu-id="ab035-107">Você pode permitir que seus usuários façam logon automaticamente no Neota Logic Studio (Logon único) com as respectivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="ab035-107">You can enable your users to automatically get signed-on to Neota Logic Studio (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ab035-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="ab035-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="ab035-109">Se você quiser saber mais detalhes sobre a integração de aplicativos SaaS com o Azure AD, consulte.</span><span class="sxs-lookup"><span data-stu-id="ab035-109">If you want to know more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="ab035-110">[O que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ab035-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ab035-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="ab035-111">Prerequisites</span></span>

<span data-ttu-id="ab035-112">Para configurar a integração do Azure AD ao Neota Logic Studio, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="ab035-112">To configure Azure AD integration with Neota Logic Studio, you need the following items:</span></span>

- <span data-ttu-id="ab035-113">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ab035-113">An Azure AD subscription</span></span>
- <span data-ttu-id="ab035-114">Uma assinatura do Neota Logic Studio habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="ab035-114">A Neota Logic Studio single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ab035-115">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="ab035-115">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ab035-116">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="ab035-116">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ab035-117">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="ab035-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ab035-118">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ab035-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ab035-119">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="ab035-119">Scenario description</span></span>

<span data-ttu-id="ab035-120">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="ab035-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ab035-121">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="ab035-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ab035-122">Adicionar o Neota Logic Studio da galeria</span><span class="sxs-lookup"><span data-stu-id="ab035-122">Adding Neota Logic Studio from the gallery</span></span>
2. <span data-ttu-id="ab035-123">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ab035-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-neota-logic-studio-from-the-gallery"></a><span data-ttu-id="ab035-124">Adicionar o Neota Logic Studio da galeria</span><span class="sxs-lookup"><span data-stu-id="ab035-124">Adding Neota Logic Studio from the gallery</span></span>

<span data-ttu-id="ab035-125">Para configurar a integração do Neota Logic Studio ao Azure AD, você precisa adicionar o do Neota Logic Studio da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="ab035-125">To configure the integration of Neota Logic Studio into Azure AD, you need to add Neota Logic Studio from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ab035-126">**Para adicionar o Neota Logic Studio da galeria, execute as etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="ab035-126">**To add Neota Logic Studio from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ab035-127">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ab035-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ab035-129">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="ab035-129">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ab035-130">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="ab035-130">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="ab035-132">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ab035-132">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="ab035-134">Na caixa de pesquisa, digite **Neota Logic Studio**.</span><span class="sxs-lookup"><span data-stu-id="ab035-134">In the search box, type **Neota Logic Studio**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_neotalogicstudio_search.png)

5. <span data-ttu-id="ab035-136">No painel de resultados, selecione **Neota Logic Studio** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ab035-136">In the results panel, select **Neota Logic Studio**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_neotalogicstudio_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ab035-138">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ab035-138">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="ab035-139">Nesta seção, você configurará e testará o logon único do Azure AD com o Neota Logic Studio, com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="ab035-139">In this section, you configure and test Azure AD single sign-on with Neota Logic Studio based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ab035-140">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Neota Logic Studio é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ab035-140">For single sign-on to work, Azure AD needs to know what the counterpart user in Neota Logic Studio is to a user in Azure AD.</span></span> <span data-ttu-id="ab035-141">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado no Neota Logic Studio.</span><span class="sxs-lookup"><span data-stu-id="ab035-141">In other words, a link relationship between an Azure AD user and the related user in Neota Logic Studio needs to be established.</span></span>

<span data-ttu-id="ab035-142">Essa relação de vínculo é estabelecida atribuindo o valor de **nome de usuário** ao Azure AD como sendo o valor de **Nome de usuário** no Neota Logic Studio.</span><span class="sxs-lookup"><span data-stu-id="ab035-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Neota Logic Studio.</span></span>

<span data-ttu-id="ab035-143">Para configurar e testar o logon único do Azure AD com o Neota Logic Studio, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="ab035-143">To configure and test Azure AD single sign-on with Neota Logic Studio, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ab035-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="ab035-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ab035-145">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="ab035-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ab035-146">**[Criar um usuário de teste do Neota Logic Studio](#creating-a-neota-logic-studio-test-user)** – para ter um equivalente de Brenda Fernandes no Neota Logic Studio que esteja vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ab035-146">**[Creating a Neota Logic Studio test user](#creating-a-neota-logic-studio-test-user)** - to have a counterpart of Britta Simon in Neota Logic Studio that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="ab035-147">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="ab035-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ab035-148">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="ab035-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ab035-149">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="ab035-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ab035-150">Nesta seção, você habilitará o logon único do Azure AD no Portal do Azure e configurará o logon único em seu aplicativo Neota Logic Studio.</span><span class="sxs-lookup"><span data-stu-id="ab035-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Neota Logic Studio application.</span></span>

<span data-ttu-id="ab035-151">**Para configurar o logon único do Azure AD com o Neota Logic Studio, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="ab035-151">**To configure Azure AD single sign-on with Neota Logic Studio, perform the following steps:**</span></span>

1. <span data-ttu-id="ab035-152">No Portal do Azure, na página de integração de aplicativos do **Neota Logic Studio**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="ab035-152">In the Azure portal, on the **Neota Logic Studio** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="ab035-154">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="ab035-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_neotalogicstudio_samlbase.png)

3. <span data-ttu-id="ab035-156">Na seção **URLs e Domínio do Neota Logic Studio**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="ab035-156">On the **Neota Logic Studio Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_neotalogicstudio_url.png)

    <span data-ttu-id="ab035-158">a.</span><span class="sxs-lookup"><span data-stu-id="ab035-158">a.</span></span> <span data-ttu-id="ab035-159">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<sub domain>.neotalogic.com/a/<sub application>`</span><span class="sxs-lookup"><span data-stu-id="ab035-159">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<sub domain>.neotalogic.com/a/<sub application>`</span></span>

    <span data-ttu-id="ab035-160">b.</span><span class="sxs-lookup"><span data-stu-id="ab035-160">b.</span></span> <span data-ttu-id="ab035-161">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<sub domain>.neotalogic.com/wb`</span><span class="sxs-lookup"><span data-stu-id="ab035-161">In the **Identifier** textbox, type a URL using the following pattern: `https://<sub domain>.neotalogic.com/wb`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ab035-162">Esses não são os valores reais.</span><span class="sxs-lookup"><span data-stu-id="ab035-162">These values are not the real.</span></span> <span data-ttu-id="ab035-163">Atualize esses valores com a URL de Entrada e o Identificador reais.</span><span class="sxs-lookup"><span data-stu-id="ab035-163">Update these values with the actual Sign-On URL & Identifier.</span></span> <span data-ttu-id="ab035-164">Aqui, sugerimos que você use o valor exclusivo de cadeia de caracteres no Identificador.</span><span class="sxs-lookup"><span data-stu-id="ab035-164">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="ab035-165">Contate a [equipe de suporte ao Cliente do Neota Logic Studio](https://www.neotalogic.com/contact-us/) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="ab035-165">Contact [Neota Logic Studio Client support team](https://www.neotalogic.com/contact-us/) to get these values.</span></span> 
 
4. <span data-ttu-id="ab035-166">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="ab035-166">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_neotalogicstudio_certificate.png) 

5. <span data-ttu-id="ab035-168">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="ab035-168">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ab035-170">Para que o SSO seja configurado para o aplicativo, entre em contato com a [equipe de suporte do Neota Logic Studio](https://www.neotalogic.com/contact-us/) e forneça a eles o arquivo **XML de metadados** baixado.</span><span class="sxs-lookup"><span data-stu-id="ab035-170">To get SSO configured for your application, Contact [Neota Logic Studio support](https://www.neotalogic.com/contact-us/) team and provide them with downloaded **Metadata XML** file.</span></span>

> [!TIP]
> <span data-ttu-id="ab035-171">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="ab035-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="ab035-172">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="ab035-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="ab035-173">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ab035-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ab035-174">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ab035-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="ab035-175">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="ab035-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="ab035-177">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="ab035-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ab035-178">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ab035-178">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-neotalogicstudio-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ab035-180">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="ab035-180">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-neotalogicstudio-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ab035-182">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ab035-182">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-neotalogicstudio-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ab035-184">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="ab035-184">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-neotalogicstudio-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ab035-186">a.</span><span class="sxs-lookup"><span data-stu-id="ab035-186">a.</span></span> <span data-ttu-id="ab035-187">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="ab035-187">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ab035-188">b.</span><span class="sxs-lookup"><span data-stu-id="ab035-188">b.</span></span> <span data-ttu-id="ab035-189">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="ab035-189">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ab035-190">c.</span><span class="sxs-lookup"><span data-stu-id="ab035-190">c.</span></span> <span data-ttu-id="ab035-191">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="ab035-191">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="ab035-192">d.</span><span class="sxs-lookup"><span data-stu-id="ab035-192">d.</span></span> <span data-ttu-id="ab035-193">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="ab035-193">Click **Create**.</span></span>
 
### <a name="creating-a-neota-logic-studio-test-user"></a><span data-ttu-id="ab035-194">Criar um usuário de teste do Neota Logic Studio</span><span class="sxs-lookup"><span data-stu-id="ab035-194">Creating a Neota Logic Studio test user</span></span>

<span data-ttu-id="ab035-195">Nesta seção, você criará um usuário chamado Brenda Fernandes no Neota Logic Studio.</span><span class="sxs-lookup"><span data-stu-id="ab035-195">In this section, you create a user called Britta Simon in Neota Logic Studio.</span></span> <span data-ttu-id="ab035-196">Trabalhe com a [equipe de suporte do cliente do Neota Logic Studio](https://www.neotalogic.com/contact-us/) para adicionar os usuários na plataforma do Neota Logic Studio.</span><span class="sxs-lookup"><span data-stu-id="ab035-196">work with [Neota Logic Studio Client support team](https://www.neotalogic.com/contact-us/) to add the users in the Neota Logic Studio platform.</span></span> <span data-ttu-id="ab035-197">Os usuários devem ser criados e ativados antes de usar o logon único.</span><span class="sxs-lookup"><span data-stu-id="ab035-197">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="ab035-198">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ab035-198">Assigning the Azure AD test user</span></span>

<span data-ttu-id="ab035-199">Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao Neota Logic Studio.</span><span class="sxs-lookup"><span data-stu-id="ab035-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Neota Logic Studio.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="ab035-201">**Para atribuir Brenda Fernandes ao Neota Logic Studio, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="ab035-201">**To assign Britta Simon to Neota Logic Studio, perform the following steps:**</span></span>

1. <span data-ttu-id="ab035-202">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="ab035-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="ab035-204">Na lista de aplicativos, escolha **Neota Logic Studio**.</span><span class="sxs-lookup"><span data-stu-id="ab035-204">In the applications list, select **Neota Logic Studio**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_neotalogicstudio_app.png) 

3. <span data-ttu-id="ab035-206">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="ab035-206">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="ab035-208">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="ab035-208">Click **Add** button.</span></span> <span data-ttu-id="ab035-209">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ab035-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="ab035-211">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="ab035-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ab035-212">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ab035-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ab035-213">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ab035-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ab035-214">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="ab035-214">Testing single sign-on</span></span>

<span data-ttu-id="ab035-215">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="ab035-215">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="ab035-216">Clique no bloco Neota Logic Studio no Painel de Acesso e você será redirecionado para a página de logon Organização.</span><span class="sxs-lookup"><span data-stu-id="ab035-216">Click the Neota Logic Studio tile in the Access Panel, you will be redirected to Organization sign-on page.</span></span> <span data-ttu-id="ab035-217">Após fazer logon com êxito, você entrará no aplicativo Neota Logic Studio.</span><span class="sxs-lookup"><span data-stu-id="ab035-217">After successful login, you will be signed-on to your Neota Logic Studio application.</span></span> <span data-ttu-id="ab035-218">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="ab035-218">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

<span data-ttu-id="ab035-219">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="ab035-219">For more information about the Access Panel, see [introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="ab035-220">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="ab035-220">Additional resources</span></span>

* [<span data-ttu-id="ab035-221">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="ab035-221">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ab035-222">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ab035-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_203.png

