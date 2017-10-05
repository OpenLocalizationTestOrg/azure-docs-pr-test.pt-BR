---
title: "Tutorial: integração do Azure Active Directory ao PlanMyLeave | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o PlanMyLeave."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b0d31cbe-7ae2-488b-9cf3-4927391fa744
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/01/2017
ms.author: jeedes
ms.openlocfilehash: ba418a641b339a0d94a3c7b2596d37fbd88a30c5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-planmyleave"></a><span data-ttu-id="fac4f-103">Tutorial: integração do Azure Active Directory com o PlanMyLeave</span><span class="sxs-lookup"><span data-stu-id="fac4f-103">Tutorial: Azure Active Directory integration with PlanMyLeave</span></span>

<span data-ttu-id="fac4f-104">Neste tutorial, você aprenderá a integrar o PlanMyLeave ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="fac4f-104">In this tutorial, you learn how to integrate PlanMyLeave with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fac4f-105">A integração do PlanMyLeave ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="fac4f-105">Integrating PlanMyLeave with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="fac4f-106">No Azure AD, você poderá controlar quem tem acesso ao PlanMyLeave</span><span class="sxs-lookup"><span data-stu-id="fac4f-106">You can control in Azure AD who has access to PlanMyLeave</span></span>
- <span data-ttu-id="fac4f-107">Você pode permitir que seus usuários façam logon automaticamente no PlanMyLeave (logon único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="fac4f-107">You can enable your users to automatically get signed-on to PlanMyLeave (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="fac4f-108">Você pode gerenciar suas contas em um único local - o portal de Gerenciamento do Azure</span><span class="sxs-lookup"><span data-stu-id="fac4f-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="fac4f-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao AD do Azure, consulte [O que é o acesso a aplicativos e logon único com o Active Directory do Azure](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="fac4f-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fac4f-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="fac4f-110">Prerequisites</span></span>

<span data-ttu-id="fac4f-111">Para configurar a integração do Azure AD com o PlanMyLeave, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="fac4f-111">To configure Azure AD integration with PlanMyLeave, you need the following items:</span></span>

- <span data-ttu-id="fac4f-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="fac4f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="fac4f-113">Uma assinatura do PlanMyLeave com logon único habilitado</span><span class="sxs-lookup"><span data-stu-id="fac4f-113">A PlanMyLeave single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="fac4f-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="fac4f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="fac4f-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="fac4f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="fac4f-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="fac4f-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="fac4f-117">Se não tiver um ambiente de avaliação do Azure AD, você poderá obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fac4f-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="fac4f-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="fac4f-118">Scenario description</span></span>
<span data-ttu-id="fac4f-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="fac4f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="fac4f-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="fac4f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fac4f-121">Adicionando PlanMyLeave da galeria</span><span class="sxs-lookup"><span data-stu-id="fac4f-121">Adding PlanMyLeave from the gallery</span></span>
2. <span data-ttu-id="fac4f-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="fac4f-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-planmyleave-from-the-gallery"></a><span data-ttu-id="fac4f-123">Adicionando PlanMyLeave da galeria</span><span class="sxs-lookup"><span data-stu-id="fac4f-123">Adding PlanMyLeave from the gallery</span></span>
<span data-ttu-id="fac4f-124">Para configurar a integração do PlanMyLeave ao Azure AD, você precisará adicionar o PlanMyLeave da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="fac4f-124">To configure the integration of PlanMyLeave into Azure AD, you need to add PlanMyLeave from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="fac4f-125">**Para adicionar o PlanMyLeave por meio da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="fac4f-125">**To add PlanMyLeave from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="fac4f-126">No **[Portal de Gerenciamento do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="fac4f-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="fac4f-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="fac4f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="fac4f-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="fac4f-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="fac4f-131">Clique em **adicionar** botão na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="fac4f-131">Click **Add** button on the top of the dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="fac4f-133">Na caixa de pesquisa, digite **PlanMyLeave**.</span><span class="sxs-lookup"><span data-stu-id="fac4f-133">In the search box, type **PlanMyLeave**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_001.png)

5. <span data-ttu-id="fac4f-135">No painel de resultados, selecione **PlanMyLeave** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="fac4f-135">In the results panel, select **PlanMyLeave**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="fac4f-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="fac4f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="fac4f-138">Nesta seção, você configurará e testará o logon único do Azure AD com o PlanMyLeave, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="fac4f-138">In this section, you configure and test Azure AD single sign-on with PlanMyLeave based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="fac4f-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do PlanMyLeave é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fac4f-139">For single sign-on to work, Azure AD needs to know what the counterpart user in PlanMyLeave is to a user in Azure AD.</span></span> <span data-ttu-id="fac4f-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado no PlanMyLeave.</span><span class="sxs-lookup"><span data-stu-id="fac4f-140">In other words, a link relationship between an Azure AD user and the related user in PlanMyLeave needs to be established.</span></span>

<span data-ttu-id="fac4f-141">Essa relação de vínculo é estabelecida atribuindo o valor de **nome de usuário** ao Azure AD como sendo o valor de **Nome de usuário** no PlanMyLeave.</span><span class="sxs-lookup"><span data-stu-id="fac4f-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in PlanMyLeave.</span></span>

<span data-ttu-id="fac4f-142">Para configurar e testar o logon único do Azure AD com o PlanMyLeave, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="fac4f-142">To configure and test Azure AD single sign-on with PlanMyLeave, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="fac4f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="fac4f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="fac4f-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** - para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="fac4f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="fac4f-145">**[Criar um usuário de teste PlanMyLeave](#creating-a-planmyleave-test-user)** – para ter um equivalente de Brenda Fernandes no PlanMyLeave que esteja vinculado à representação dela no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fac4f-145">**[Creating a PlanMyLeave test user](#creating-a-planmyleave-test-user)** - to have a counterpart of Britta Simon in PlanMyLeave that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="fac4f-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** - para habilitar Britta Simon a usar o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="fac4f-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="fac4f-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="fac4f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="fac4f-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="fac4f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="fac4f-149">Nesta seção, você habilita o logon único do Azure AD no Portal de Gerenciamento do Azure e configura o logon único em seu aplicativo PlanMyLeave.</span><span class="sxs-lookup"><span data-stu-id="fac4f-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your PlanMyLeave application.</span></span>

<span data-ttu-id="fac4f-150">**Para configurar o logon único do Azure AD com o PlanMyLeave, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="fac4f-150">**To configure Azure AD single sign-on with PlanMyLeave, perform the following steps:**</span></span>

1. <span data-ttu-id="fac4f-151">No Portal de Gerenciamento do Azure, na página de integração de aplicativos do **PlanMyLeave**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="fac4f-151">In the Azure Management portal, on the **PlanMyLeave** application integration page, click **Single sign-on**.</span></span>

    ![Configurar o logon único][4]

2. <span data-ttu-id="fac4f-153">Na página da caixa de diálogo **Logon único**, como **Modo**, selecione **Logon com base em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="fac4f-153">On the **Single sign-on** dialog page, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configurar o logon único](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_01.png)

3. <span data-ttu-id="fac4f-155">Na seção **URLs e Domínio do PlanMyLeave**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="fac4f-155">On the **PlanMyLeave Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_02.png)

    <span data-ttu-id="fac4f-157">a.</span><span class="sxs-lookup"><span data-stu-id="fac4f-157">a.</span></span> <span data-ttu-id="fac4f-158">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<company-name>.planmyleave.com/Login.aspx`</span><span class="sxs-lookup"><span data-stu-id="fac4f-158">In the **Sign On URL** textbox, type a URL using the following pattern: `https://<company-name>.planmyleave.com/Login.aspx`</span></span>
    
    <span data-ttu-id="fac4f-159">b.</span><span class="sxs-lookup"><span data-stu-id="fac4f-159">b.</span></span> <span data-ttu-id="fac4f-160">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<company-name>.planmyleave.com`</span><span class="sxs-lookup"><span data-stu-id="fac4f-160">In the **Identifer** textbox, type a URL using the following pattern: `https://<company-name>.planmyleave.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="fac4f-161">Observe que esses não são os valores reais.</span><span class="sxs-lookup"><span data-stu-id="fac4f-161">Please note that these are not the real values.</span></span> <span data-ttu-id="fac4f-162">É necessário atualizar esses valores com a URL de Entrada e o Identificador reais.</span><span class="sxs-lookup"><span data-stu-id="fac4f-162">You have to update these values with the actual Sign On URL and Identifier.</span></span> <span data-ttu-id="fac4f-163">Para obter esses valores, entre em contato com a [equipe de suporte do PlanMyLeave](mailto:support@planmyleave.com).</span><span class="sxs-lookup"><span data-stu-id="fac4f-163">Contact [PlanMyLeave support team](mailto:support@planmyleave.com) to get these values.</span></span>

4. <span data-ttu-id="fac4f-164">Sobre o **certificado de autenticação SAML** seção, clique em **criar novo certificado**.</span><span class="sxs-lookup"><span data-stu-id="fac4f-164">On the **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_03.png)     

5. <span data-ttu-id="fac4f-166">Na caixa de diálogo **Criar um Novo Certificado**, clique no ícone de calendário e selecione uma **data de expiração**.</span><span class="sxs-lookup"><span data-stu-id="fac4f-166">On the **Create New Certificate** dialog, click the calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="fac4f-167">Em seguida, clique no botão **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="fac4f-167">Then click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-planmyleave-tutorial/tutorial_general_300.png)

6. <span data-ttu-id="fac4f-169">Na seção **Certificado de Autenticação SAML**, selecione **Ativar o novo certificado** e clique no botão **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="fac4f-169">On the **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_04.png)

7. <span data-ttu-id="fac4f-171">Na janela pop-up **Certificado de substituição**, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="fac4f-171">On the pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-planmyleave-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="fac4f-173">Na seção **Certificado de Autenticação SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado em seu computador.</span><span class="sxs-lookup"><span data-stu-id="fac4f-173">On the **SAML Signing Certificate** section, click **Certificate (base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_05.png) 

9. <span data-ttu-id="fac4f-175">Na seção **Configuração do PlanMyLeave**, clique em **Configurar PlanMyLeave** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="fac4f-175">On the **PlanMyLeave Configuration** section, click **Configure PlanMyLeave** to open **Configure sign-on** window.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_06.png) 

    ![Configurar Logon Único](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_07.png)

10. <span data-ttu-id="fac4f-178">Em outra janela do navegador da Web, faça logon no locatário do PlanMyLeave como administrador.</span><span class="sxs-lookup"><span data-stu-id="fac4f-178">In a different web browser window, log into your PlanMyLeave tenant as an administrator.</span></span>

11. <span data-ttu-id="fac4f-179">Acesse **Configuração do Sistema**.</span><span class="sxs-lookup"><span data-stu-id="fac4f-179">Go to **System Setup**.</span></span> <span data-ttu-id="fac4f-180">Em seguida, na seção **Gerenciamento de Segurança**, clique em **Configurações do SAML da Empresa**.</span><span class="sxs-lookup"><span data-stu-id="fac4f-180">Then on the **Security Management** section click **Company SAML settings** .</span></span>

    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_002.png) 

12. <span data-ttu-id="fac4f-182">Na seção **Configurações de SAML**, clique no ícone do editor.</span><span class="sxs-lookup"><span data-stu-id="fac4f-182">On the **SAML Settings** section, click editor icon.</span></span>

    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_003.png)

13. <span data-ttu-id="fac4f-184">Na seção **Atualizar Configuração do SAML**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="fac4f-184">On the **Update SAML Settings** section, perform the following steps:</span></span>

    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_004.png)

    <span data-ttu-id="fac4f-186">a.</span><span class="sxs-lookup"><span data-stu-id="fac4f-186">a.</span></span>  <span data-ttu-id="fac4f-187">Na caixa de texto **URL de Logon**, insira o valor da **URL de Serviço de Logon Único SAML** do assistente de configuração de aplicativo do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fac4f-187">In the **Login URL** textbox, put the value of **SAML Single Sign-On Service URL** from Azure AD application configuration window.</span></span>

    <span data-ttu-id="fac4f-188">b.</span><span class="sxs-lookup"><span data-stu-id="fac4f-188">b.</span></span>  <span data-ttu-id="fac4f-189">Abra seu arquivo de certificado baixado no bloco de notas, copie somente o conteúdo entre ---Begin Certificate--- e ---End certificate---- na área de transferência e cole-o na caixa de texto **Certificado**.</span><span class="sxs-lookup"><span data-stu-id="fac4f-189">Open your downloaded certificate file in notepad, copy only the content between the ---Begin Certificate--- and ---End certificate---- of it into your clipboard, and then paste it to the **Certificate** textbox.</span></span>

    <span data-ttu-id="fac4f-190">c.</span><span class="sxs-lookup"><span data-stu-id="fac4f-190">c.</span></span> <span data-ttu-id="fac4f-191">Defina "**Is Enable**" como "**Yes**".</span><span class="sxs-lookup"><span data-stu-id="fac4f-191">Set "**Is Enable**" to "**Yes**".</span></span>

    <span data-ttu-id="fac4f-192">d.</span><span class="sxs-lookup"><span data-stu-id="fac4f-192">d.</span></span> <span data-ttu-id="fac4f-193">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="fac4f-193">Click **Save**.</span></span>



### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="fac4f-194">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="fac4f-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="fac4f-195">O objetivo desta seção é criar um usuário de teste no Portal de Gerenciamento do Azure chamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fac4f-195">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="fac4f-197">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="fac4f-197">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="fac4f-198">No **portal de Gerenciamento do Azure**, no painel navegação à esquerda, clique em **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="fac4f-198">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="fac4f-200">Vá para **usuários e grupos** e clique em **todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="fac4f-200">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="fac4f-202">Na parte superior da caixa de diálogo clique **adicionar** para abrir o **usuário** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="fac4f-202">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="fac4f-204">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="fac4f-204">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="fac4f-206">a.</span><span class="sxs-lookup"><span data-stu-id="fac4f-206">a.</span></span> <span data-ttu-id="fac4f-207">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="fac4f-207">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="fac4f-208">b.</span><span class="sxs-lookup"><span data-stu-id="fac4f-208">b.</span></span> <span data-ttu-id="fac4f-209">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="fac4f-209">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="fac4f-210">c.</span><span class="sxs-lookup"><span data-stu-id="fac4f-210">c.</span></span> <span data-ttu-id="fac4f-211">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="fac4f-211">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="fac4f-212">d.</span><span class="sxs-lookup"><span data-stu-id="fac4f-212">d.</span></span> <span data-ttu-id="fac4f-213">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="fac4f-213">Click **Create**.</span></span> 



### <a name="creating-a-planmyleave-test-user"></a><span data-ttu-id="fac4f-214">Criação de um usuário de teste PlanMyLeave</span><span class="sxs-lookup"><span data-stu-id="fac4f-214">Creating a PlanMyLeave test user</span></span>

<span data-ttu-id="fac4f-215">O objetivo desta seção é criar um usuário chamado Brenda Fernandes no PlanMyLeave.</span><span class="sxs-lookup"><span data-stu-id="fac4f-215">The objective of this section is to create a user called Britta Simon in PlanMyLeave.</span></span> <span data-ttu-id="fac4f-216">O PlanMyLeave dá suporte ao provisionamento just-in-time, que está habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="fac4f-216">PlanMyLeave supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="fac4f-217">Não há itens de ação para você nesta seção.</span><span class="sxs-lookup"><span data-stu-id="fac4f-217">There is no action item for you in this section.</span></span> <span data-ttu-id="fac4f-218">Um novo usuário será criado durante uma tentativa de acessar o PlanMyLeave, caso ainda não exista.</span><span class="sxs-lookup"><span data-stu-id="fac4f-218">A new user will be created during an attempt to access PlanMyLeave if it doesn't exist yet.</span></span>

> [!NOTE]
> <span data-ttu-id="fac4f-219">Se precisar criar um usuário manualmente, entre em contato com a [equipe de suporte do PlanMyLeave](mailto:support@planmyleave.com).</span><span class="sxs-lookup"><span data-stu-id="fac4f-219">If you need to create an user manually, you need to contact [PlanMyLeave support team](mailto:support@planmyleave.com).</span></span>



### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="fac4f-220">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="fac4f-220">Assigning the Azure AD test user</span></span>

<span data-ttu-id="fac4f-221">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure, concedendo a ela acesso ao PlanMyLeave.</span><span class="sxs-lookup"><span data-stu-id="fac4f-221">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to PlanMyLeave.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="fac4f-223">**Para atribuir Brenda Fernandes ao PlanMyLeave, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="fac4f-223">**To assign Britta Simon to PlanMyLeave, perform the following steps:**</span></span>

1. <span data-ttu-id="fac4f-224">No portal de gerenciamento do Azure, abra a exibição de aplicativos e, em seguida, navegue até o modo de exibição de diretório e vá para **aplicativos empresariais** e clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="fac4f-224">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="fac4f-226">Na lista de aplicativos, selecione **PlanMyLeave**.</span><span class="sxs-lookup"><span data-stu-id="fac4f-226">In the applications list, select **PlanMyLeave**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_50.png) 

3. <span data-ttu-id="fac4f-228">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="fac4f-228">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="fac4f-230">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="fac4f-230">Click **Add** button.</span></span> <span data-ttu-id="fac4f-231">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="fac4f-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="fac4f-233">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="fac4f-233">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="fac4f-234">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="fac4f-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="fac4f-235">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="fac4f-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="fac4f-236">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="fac4f-236">Testing single sign-on</span></span>

<span data-ttu-id="fac4f-237">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="fac4f-237">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="fac4f-238">Ao clicar no bloco PlanMyLeave no Painel de Acesso, você deverá ser conectado automaticamente a seu aplicativo PlanMyLeave.</span><span class="sxs-lookup"><span data-stu-id="fac4f-238">When you click the PlanMyLeave tile in the Access Panel, you should get automatically signed-on to your PlanMyLeave application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="fac4f-239">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="fac4f-239">Additional resources</span></span>

* [<span data-ttu-id="fac4f-240">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="fac4f-240">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fac4f-241">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="fac4f-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_203.png