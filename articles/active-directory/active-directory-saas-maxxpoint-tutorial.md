---
title: "Tutorial: Integração do Azure Active Directory ao MaxxPoint | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o MaxxPoint."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 15ba026e-96fc-4ae8-b135-0169da810e99
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/13/2017
ms.author: jeedes
ms.openlocfilehash: 8a7481b71df5ca407dbed5da3d3cc26991504c82
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-maxxpoint"></a><span data-ttu-id="d16ed-103">Tutorial: Integração do Azure Active Directory ao MaxxPoint</span><span class="sxs-lookup"><span data-stu-id="d16ed-103">Tutorial: Azure Active Directory integration with MaxxPoint</span></span>

<span data-ttu-id="d16ed-104">Neste tutorial, você aprenderá a integrar o MaxxPoint ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="d16ed-104">In this tutorial, you learn how to integrate MaxxPoint with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d16ed-105">A integração do MaxxPoint ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="d16ed-105">Integrating MaxxPoint with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d16ed-106">No Azure AD, é possível controlar quem tem acesso ao MaxxPoint</span><span class="sxs-lookup"><span data-stu-id="d16ed-106">You can control in Azure AD who has access to MaxxPoint</span></span>
- <span data-ttu-id="d16ed-107">Você pode permitir que seus usuários façam logon automaticamente no MaxxPoint (logon único) com as contas do Azure AD deles</span><span class="sxs-lookup"><span data-stu-id="d16ed-107">You can enable your users to automatically get signed-on to MaxxPoint (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d16ed-108">Você pode gerenciar suas contas em um único local: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="d16ed-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="d16ed-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d16ed-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d16ed-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="d16ed-110">Prerequisites</span></span>

<span data-ttu-id="d16ed-111">Para configurar a integração do Azure AD ao MaxxPoint, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="d16ed-111">To configure Azure AD integration with MaxxPoint, you need the following items:</span></span>

- <span data-ttu-id="d16ed-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d16ed-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d16ed-113">Uma assinatura habilitada para logon único do MaxxPoint</span><span class="sxs-lookup"><span data-stu-id="d16ed-113">A MaxxPoint single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d16ed-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="d16ed-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d16ed-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="d16ed-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d16ed-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="d16ed-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="d16ed-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d16ed-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d16ed-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="d16ed-118">Scenario description</span></span>
<span data-ttu-id="d16ed-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="d16ed-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d16ed-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="d16ed-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d16ed-121">Adicionar o MaxxPoint da galeria</span><span class="sxs-lookup"><span data-stu-id="d16ed-121">Adding MaxxPoint from the gallery</span></span>
2. <span data-ttu-id="d16ed-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d16ed-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-maxxpoint-from-the-gallery"></a><span data-ttu-id="d16ed-123">Adicionar o MaxxPoint da galeria</span><span class="sxs-lookup"><span data-stu-id="d16ed-123">Adding MaxxPoint from the gallery</span></span>
<span data-ttu-id="d16ed-124">Para configurar a integração do MaxxPoint ao Azure AD, você precisará adicionar o MaxxPoint à sua lista de aplicativos SaaS gerenciados por meio da galeria.</span><span class="sxs-lookup"><span data-stu-id="d16ed-124">To configure the integration of MaxxPoint into Azure AD, you need to add MaxxPoint from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d16ed-125">**Para adicionar o MaxxPoint da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="d16ed-125">**To add MaxxPoint from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d16ed-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d16ed-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d16ed-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="d16ed-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d16ed-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="d16ed-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="d16ed-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d16ed-131">Click **New application** button on the top of dialog to add new application.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="d16ed-133">Na caixa de pesquisa, digite **MaxxPoint**.</span><span class="sxs-lookup"><span data-stu-id="d16ed-133">In the search box, type **MaxxPoint**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-maxxpoint-tutorial/tutorial_maxxpoint_001.png)

5. <span data-ttu-id="d16ed-135">No painel de resultados, selecione **MaxxPoint** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d16ed-135">In the results panel, select **MaxxPoint**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-maxxpoint-tutorial/tutorial_maxxpoint_0001.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d16ed-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d16ed-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d16ed-138">Nesta seção, você vai configurar e testar o logon único do Azure AD com o MaxxPoint com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="d16ed-138">In this section, you configure and test Azure AD single sign-on with MaxxPoint based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d16ed-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do MaxxPoint é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d16ed-139">For single sign-on to work, Azure AD needs to know what the counterpart user in MaxxPoint is to a user in Azure AD.</span></span> <span data-ttu-id="d16ed-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do MaxxPoint.</span><span class="sxs-lookup"><span data-stu-id="d16ed-140">In other words, a link relationship between an Azure AD user and the related user in MaxxPoint needs to be established.</span></span>

<span data-ttu-id="d16ed-141">Essa relação de vínculo é estabelecida atribuindo o valor de **nome de usuário** no Azure AD como sendo o valor de **Nome de Usuário** no MaxxPoint.</span><span class="sxs-lookup"><span data-stu-id="d16ed-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in MaxxPoint.</span></span>

<span data-ttu-id="d16ed-142">Para configurar e testar o logon único do Azure AD com o MaxxPoint, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="d16ed-142">To configure and test Azure AD single sign-on with MaxxPoint, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d16ed-143">**[Configuração do Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="d16ed-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d16ed-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** - para testar logon único do Azure AD com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d16ed-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d16ed-145">**[Criar um usuário de teste do MaxxPoint](#creating-a-maxxpoint-test-user)** — para ter um equivalente de Brenda Fernandes no MaxxPoint que esteja vinculado à representação dela no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d16ed-145">**[Creating a MaxxPoint test user](#creating-a-maxxpoint-test-user)** - to have a counterpart of Britta Simon in MaxxPoint that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="d16ed-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** - para habilitar Britta Simon a usar o logon único do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d16ed-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d16ed-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="d16ed-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d16ed-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="d16ed-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d16ed-149">Nesta seção, você habilita o logon único do Azure AD no Portal do Azure e configura o logon único em seu aplicativo MaxxPoint.</span><span class="sxs-lookup"><span data-stu-id="d16ed-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your MaxxPoint application.</span></span>

<span data-ttu-id="d16ed-150">**Para configurar o logon único do Azure AD com o MaxxPoint, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="d16ed-150">**To configure Azure AD single sign-on with MaxxPoint, perform the following steps:**</span></span>

1. <span data-ttu-id="d16ed-151">No Portal do Azure, na página de integração de aplicativos do **MaxxPoint**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="d16ed-151">In the Azure portal, on the **MaxxPoint** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="d16ed-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="d16ed-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_300.png)

3. <span data-ttu-id="d16ed-155">Na seção **Domínio e URLs do MaxxPoint**, se você quiser configurar o aplicativo no **Modo iniciado por IDP**, não é necessário executar qualquer etapa.</span><span class="sxs-lookup"><span data-stu-id="d16ed-155">On the **MaxxPoint Domain and URLs** section, If you wish to configure the application in **IDP initiated mode**, no need to perform any steps.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-maxxpoint-tutorial/tutorial_maxxpoint_02.png)
    
4. <span data-ttu-id="d16ed-157">Na seção **Domínio e URLs do MaxxPoint**, se você quiser configurar o aplicativo no **Modo iniciado por SP**, não é necessário executar qualquer etapa:</span><span class="sxs-lookup"><span data-stu-id="d16ed-157">On the **MaxxPoint Domain and URLs** section, If you wish to configure the application in **SP initiated mode**, perform the following steps:</span></span>
    
    ![Configurar o logon único](./media/active-directory-saas-maxxpoint-tutorial/tutorial_maxxpoint_03.png)

    <span data-ttu-id="d16ed-159">a.</span><span class="sxs-lookup"><span data-stu-id="d16ed-159">a.</span></span> <span data-ttu-id="d16ed-160">Clique na opção **Mostrar configurações avançadas de URL**</span><span class="sxs-lookup"><span data-stu-id="d16ed-160">Click **Show advanced URL settings** option</span></span>

    <span data-ttu-id="d16ed-161">b.</span><span class="sxs-lookup"><span data-stu-id="d16ed-161">b.</span></span> <span data-ttu-id="d16ed-162">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://maxxpoint.westipc.com/default/sso/login/entity/<customer-id>-azure`</span><span class="sxs-lookup"><span data-stu-id="d16ed-162">In the **Sign On URL** textbox, type a URL using the following pattern: `https://maxxpoint.westipc.com/default/sso/login/entity/<customer-id>-azure`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d16ed-163">Observe que esse não é o valor real.</span><span class="sxs-lookup"><span data-stu-id="d16ed-163">Please note that this is not the real value.</span></span> <span data-ttu-id="d16ed-164">Você precisa atualizar esse valor com a URL de Entrada real.</span><span class="sxs-lookup"><span data-stu-id="d16ed-164">You have to update this value with the actual Sign On URL.</span></span> <span data-ttu-id="d16ed-165">Ligue para a equipe do MaxxPoint **888-728-0950** para obter esse valor.</span><span class="sxs-lookup"><span data-stu-id="d16ed-165">Call MaxxPoint team on **888-728-0950** to get this value.</span></span>

5. <span data-ttu-id="d16ed-166">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="d16ed-166">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-maxxpoint-tutorial/tutorial_maxxpoint_06.png) 

6. <span data-ttu-id="d16ed-168">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="d16ed-168">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="d16ed-170">Para obter o SSO configurado para seu aplicativo, ligue para a equipe de suporte do MaxxPoint no número **888-728-0950** e ela irá ajudá-lo sobre como disponibilizar o arquivo **XML de Metadados** baixado.</span><span class="sxs-lookup"><span data-stu-id="d16ed-170">To get SSO configured for your application, call MaxxPoint support team on **888-728-0950** and they'll assist you further on how to provide them the downloaded **Metadata XML** file.</span></span> 

> [!TIP]
> <span data-ttu-id="d16ed-171">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="d16ed-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d16ed-172">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, simplesmente clique na guia **Logon Único** e acesse a documentação inserida através da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="d16ed-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d16ed-173">Saiba mais sobre o recurso de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d16ed-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d16ed-174">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d16ed-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="d16ed-175">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="d16ed-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="d16ed-177">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="d16ed-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d16ed-178">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d16ed-178">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-maxxpoint-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d16ed-180">Vá para **usuários e grupos** e clique em **todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="d16ed-180">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-maxxpoint-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d16ed-182">Na parte superior da caixa de diálogo clique **adicionar** para abrir o **usuário** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d16ed-182">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-maxxpoint-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d16ed-184">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="d16ed-184">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-maxxpoint-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d16ed-186">a.</span><span class="sxs-lookup"><span data-stu-id="d16ed-186">a.</span></span> <span data-ttu-id="d16ed-187">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="d16ed-187">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d16ed-188">b.</span><span class="sxs-lookup"><span data-stu-id="d16ed-188">b.</span></span> <span data-ttu-id="d16ed-189">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="d16ed-189">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d16ed-190">c.</span><span class="sxs-lookup"><span data-stu-id="d16ed-190">c.</span></span> <span data-ttu-id="d16ed-191">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="d16ed-191">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d16ed-192">d.</span><span class="sxs-lookup"><span data-stu-id="d16ed-192">d.</span></span> <span data-ttu-id="d16ed-193">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="d16ed-193">Click **Create**.</span></span> 

### <a name="creating-a-maxxpoint-test-user"></a><span data-ttu-id="d16ed-194">Criar um usuário de teste do MaxxPoint</span><span class="sxs-lookup"><span data-stu-id="d16ed-194">Creating a MaxxPoint test user</span></span>

<span data-ttu-id="d16ed-195">Nesta seção, você criará uma usuária chamada Brenda Fernandes no MaxxPoint.</span><span class="sxs-lookup"><span data-stu-id="d16ed-195">In this section, you create a user called Britta Simon in MaxxPoint.</span></span> <span data-ttu-id="d16ed-196">Ligue para a equipe de suporte do MaxxPoint no número **888-728-0950** para adicionar os usuários no aplicativo MaxxPoint.</span><span class="sxs-lookup"><span data-stu-id="d16ed-196">Please call MaxxPoint support team on **888-728-0950** to add the users in the MaxxPoint application.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="d16ed-197">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d16ed-197">Assigning the Azure AD test user</span></span>

<span data-ttu-id="d16ed-198">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao MaxxPoint.</span><span class="sxs-lookup"><span data-stu-id="d16ed-198">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to MaxxPoint.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="d16ed-200">**Para atribuir Brenda Fernandes ao MaxxPoint, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="d16ed-200">**To assign Britta Simon to MaxxPoint, perform the following steps:**</span></span>

1. <span data-ttu-id="d16ed-201">No portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="d16ed-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="d16ed-203">Na lista de aplicativos, selecione **MaxxPoint**.</span><span class="sxs-lookup"><span data-stu-id="d16ed-203">In the applications list, select **MaxxPoint**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-maxxpoint-tutorial/tutorial_maxxpoint_50.png) 

3. <span data-ttu-id="d16ed-205">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="d16ed-205">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="d16ed-207">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="d16ed-207">Click **Add** button.</span></span> <span data-ttu-id="d16ed-208">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d16ed-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="d16ed-210">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="d16ed-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d16ed-211">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d16ed-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d16ed-212">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d16ed-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d16ed-213">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="d16ed-213">Testing single sign-on</span></span>

<span data-ttu-id="d16ed-214">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="d16ed-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="d16ed-215">Ao clicar no bloco do MaxxPoint no Painel de Acesso, você deverá ser conectado automaticamente ao seu aplicativo MaxxPoint.</span><span class="sxs-lookup"><span data-stu-id="d16ed-215">When you click the MaxxPoint tile in the Access Panel, you should get automatically signed-on to your MaxxPoint application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="d16ed-216">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="d16ed-216">Additional resources</span></span>

* [<span data-ttu-id="d16ed-217">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="d16ed-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d16ed-218">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d16ed-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_203.png