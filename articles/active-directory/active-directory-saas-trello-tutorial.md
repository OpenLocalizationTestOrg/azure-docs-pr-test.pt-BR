---
title: "Tutorial: integração do Azure Active Directory ao Trello | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Trello."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: cd5ae365-9ed6-43a6-920b-f7814b993949
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: d93667f16f2d72995e4a42e79e9125b8e3f6b07c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-trello"></a><span data-ttu-id="17998-103">Tutorial: integração do Azure Active Directory ao Trello</span><span class="sxs-lookup"><span data-stu-id="17998-103">Tutorial: Azure Active Directory integration with Trello</span></span>

<span data-ttu-id="17998-104">Neste tutorial, você aprenderá a integrar o Trello ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="17998-104">In this tutorial, you learn how to integrate Trello with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="17998-105">A integração do Trello ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="17998-105">Integrating Trello with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="17998-106">Você pode controlar no Azure AD quem tem acesso ao Trello</span><span class="sxs-lookup"><span data-stu-id="17998-106">You can control in Azure AD who has access to Trello</span></span>
- <span data-ttu-id="17998-107">Você pode permitir que usuários façam logon automaticamente no Trello (Logon Único) com as respectivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="17998-107">You can enable your users to automatically get signed-on to Trello (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="17998-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="17998-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="17998-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="17998-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="17998-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="17998-110">Prerequisites</span></span>

<span data-ttu-id="17998-111">Para configurar a integração do Azure AD ao Trello, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="17998-111">To configure Azure AD integration with Trello, you need the following items:</span></span>

- <span data-ttu-id="17998-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="17998-112">An Azure AD subscription</span></span>
- <span data-ttu-id="17998-113">Uma assinatura do Trello habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="17998-113">A Trello single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="17998-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="17998-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="17998-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="17998-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="17998-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="17998-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="17998-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="17998-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="17998-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="17998-118">Scenario description</span></span>
<span data-ttu-id="17998-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="17998-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="17998-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="17998-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="17998-121">Adicionando o Trello da galeria</span><span class="sxs-lookup"><span data-stu-id="17998-121">Adding Trello from the gallery</span></span>
2. <span data-ttu-id="17998-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="17998-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-trello-from-the-gallery"></a><span data-ttu-id="17998-123">Adicionando o Trello da galeria</span><span class="sxs-lookup"><span data-stu-id="17998-123">Adding Trello from the gallery</span></span>
<span data-ttu-id="17998-124">Para configurar a integração do Trello ao Azure AD, você precisará adicionar o Trello da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="17998-124">To configure the integration of Trello into Azure AD, you need to add Trello from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="17998-125">**Para adicionar o Trello da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="17998-125">**To add Trello from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="17998-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="17998-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="17998-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="17998-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="17998-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="17998-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="17998-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="17998-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="17998-133">Na caixa de pesquisa, digite **Trello**.</span><span class="sxs-lookup"><span data-stu-id="17998-133">In the search box, type **Trello**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-trello-tutorial/tutorial_trello_search.png)

5. <span data-ttu-id="17998-135">No painel de resultados, selecione **Trello** e, em seguida, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="17998-135">In the results panel, select **Trello**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-trello-tutorial/tutorial_trello_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="17998-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="17998-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="17998-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Trello, com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="17998-138">In this section, you configure and test Azure AD single sign-on with Trello based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="17998-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Trello é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="17998-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Trello is to a user in Azure AD.</span></span> <span data-ttu-id="17998-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Trello.</span><span class="sxs-lookup"><span data-stu-id="17998-140">In other words, a link relationship between an Azure AD user and the related user in Trello needs to be established.</span></span>

<span data-ttu-id="17998-141">No Trello, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="17998-141">In Trello, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="17998-142">Para configurar e testar o logon único do Azure AD com o Trello, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="17998-142">To configure and test Azure AD single sign-on with Trello, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="17998-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="17998-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="17998-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="17998-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="17998-145">**[Criação de um usuário de teste do Trello](#creating-a-trello-test-user)** – para ter um equivalente de Brenda Fernandes no Trello que esteja vinculado à representação de usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="17998-145">**[Creating a Trello test user](#creating-a-trello-test-user)** - to have a counterpart of Britta Simon in Trello that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="17998-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="17998-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="17998-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="17998-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="17998-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="17998-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="17998-149">Nesta seção, você habilitará o logon único do Azure AD no Portal do Azure e configurará o logon único no aplicativo Trello.</span><span class="sxs-lookup"><span data-stu-id="17998-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Trello application.</span></span>

<span data-ttu-id="17998-150">**Para configurar o logon único do Azure AD com o Trello, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="17998-150">**To configure Azure AD single sign-on with Trello, perform the following steps:**</span></span>

1. <span data-ttu-id="17998-151">No Portal do Azure, na página de integração de aplicativos do **Trello**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="17998-151">In the Azure portal, on the **Trello** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="17998-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="17998-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-trello-tutorial/tutorial_trello_samlbase.png)

3. <span data-ttu-id="17998-155">Na seção **URLs e Domínio do Trello**, se você desejar configurar o aplicativo no **modo iniciado pelo IDP**, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="17998-155">On the **Trello Domain and URLs** section, If you wish to configure the application in **IDP initiated mode**, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-trello-tutorial/tutorial_trello_url.png)

    <span data-ttu-id="17998-157">Na caixa de texto **URL de resposta**, digite uma URL no seguinte padrão: `https://trello.com/auth/saml/consume/<enterprise>`</span><span class="sxs-lookup"><span data-stu-id="17998-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://trello.com/auth/saml/consume/<enterprise>`</span></span>

4. <span data-ttu-id="17998-158">Na seção **URLs e Domínio do Trello**, se você desejar configurar o aplicativo no **modo iniciado pelo SP**, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="17998-158">On the **Trello Domain and URLs** section, If you wish to configure the application in **SP initiated mode**, perform the following steps:</span></span>
    
    ![Configurar Logon Único](./media/active-directory-saas-trello-tutorial/tutorial_trello_url1.png)

    <span data-ttu-id="17998-160">a.</span><span class="sxs-lookup"><span data-stu-id="17998-160">a.</span></span> <span data-ttu-id="17998-161">Clique em **Mostrar configurações de URL avançadas**.</span><span class="sxs-lookup"><span data-stu-id="17998-161">Click on the **Show advanced URL settings**.</span></span>

    <span data-ttu-id="17998-162">b.</span><span class="sxs-lookup"><span data-stu-id="17998-162">b.</span></span> <span data-ttu-id="17998-163">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://trello.com/auth/saml/consume/<enterprise>`</span><span class="sxs-lookup"><span data-stu-id="17998-163">In the **Sign On URL** textbox, type a URL using the following pattern: `https://trello.com/auth/saml/consume/<enterprise>`</span></span>

    >[!NOTE]
    ><span data-ttu-id="17998-164">Você deve obter o campo de dados dinâmico **\<empresa\>** do Trello.</span><span class="sxs-lookup"><span data-stu-id="17998-164">You should get the **\<enterprise\>** slug from Trello.</span></span> <span data-ttu-id="17998-165">Se você não tiver o valor do campo de dados dinâmico, contate a [equipe de suporte do Trello](mailto:support@trello.com) a fim de obtê-lo para sua empresa.</span><span class="sxs-lookup"><span data-stu-id="17998-165">If you don't have the slug value, contact [Trello support team](mailto:support@trello.com) to get the slug for you enterprise.</span></span>
    > 

5. <span data-ttu-id="17998-166">O aplicativo Trello espera que as asserções SAML contenham atributos específicos.</span><span class="sxs-lookup"><span data-stu-id="17998-166">Trello application expects the SAML assertions to contain specific attributes.</span></span> <span data-ttu-id="17998-167">Configure as atribuições a seguir para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="17998-167">Configure the following attributes  for this application.</span></span> <span data-ttu-id="17998-168">É possível gerenciar os valores desses atributos em **“Atributos de Usuário”** do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="17998-168">You can manage the values of these attributes from the **"User Attributes"** of the application.</span></span> <span data-ttu-id="17998-169">A captura de tela a seguir mostra um exemplo disso.</span><span class="sxs-lookup"><span data-stu-id="17998-169">The following screenshot shows an example for this.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-trello-tutorial/tutorial_trello_attribute.png)

6. <span data-ttu-id="17998-171">Na caixa de diálogo **Atributos de token SAML** , para cada linha mostrada na tabela a seguir, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="17998-171">On the **SAML token attributes** dialog, for each row shown in the table below, perform the following steps:</span></span>
 
    | <span data-ttu-id="17998-172">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="17998-172">Attribute Name</span></span> | <span data-ttu-id="17998-173">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="17998-173">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="17998-174">User.Email</span><span class="sxs-lookup"><span data-stu-id="17998-174">User.Email</span></span> | <span data-ttu-id="17998-175">user.mail</span><span class="sxs-lookup"><span data-stu-id="17998-175">user.mail</span></span> |
    | <span data-ttu-id="17998-176">User.FirstName</span><span class="sxs-lookup"><span data-stu-id="17998-176">User.FirstName</span></span> | <span data-ttu-id="17998-177">user.givenname</span><span class="sxs-lookup"><span data-stu-id="17998-177">user.givenname</span></span> |
    | <span data-ttu-id="17998-178">User.LastName</span><span class="sxs-lookup"><span data-stu-id="17998-178">User.LastName</span></span> | <span data-ttu-id="17998-179">user.surname</span><span class="sxs-lookup"><span data-stu-id="17998-179">user.surname</span></span> |

    <span data-ttu-id="17998-180">a.</span><span class="sxs-lookup"><span data-stu-id="17998-180">a.</span></span> <span data-ttu-id="17998-181">Clique em **Adicionar atributo** para abrir o diálogo **Adicionar Atributo**.</span><span class="sxs-lookup"><span data-stu-id="17998-181">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-trello-tutorial/tutorial_officespace_04.png)

    ![Configurar Logon Único](./media/active-directory-saas-trello-tutorial/tutorial_officespace_05.png)

    <span data-ttu-id="17998-184">b.</span><span class="sxs-lookup"><span data-stu-id="17998-184">b.</span></span> <span data-ttu-id="17998-185">Na caixa de texto **Nome** , digite o nome do atributo mostrado para essa linha.</span><span class="sxs-lookup"><span data-stu-id="17998-185">In the **Name** textbox, type the attribute name shown for that row.</span></span> 

    <span data-ttu-id="17998-186">c.</span><span class="sxs-lookup"><span data-stu-id="17998-186">c.</span></span> <span data-ttu-id="17998-187">Na lista **Valor**, digite o valor do atributo mostrado para essa linha.</span><span class="sxs-lookup"><span data-stu-id="17998-187">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="17998-188">d.</span><span class="sxs-lookup"><span data-stu-id="17998-188">d.</span></span> <span data-ttu-id="17998-189">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="17998-189">Click **Ok**.</span></span> 
 
7. <span data-ttu-id="17998-190">Na seção **Certificado de Autenticação SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado em seu computador.</span><span class="sxs-lookup"><span data-stu-id="17998-190">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-trello-tutorial/tutorial_trello_certificate.png) 

8. <span data-ttu-id="17998-192">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="17998-192">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-trello-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="17998-194">Na seção **Configuração do Trello**, clique em **Configurar o Trello** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="17998-194">On the **Trello Configuration** section, click **Configure Trello** to open **Configure sign-on** window.</span></span> <span data-ttu-id="17998-195">Copie a **URL de serviço de logon único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="17998-195">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-trello-tutorial/tutorial_trello_configure.png) 

9. <span data-ttu-id="17998-197">Para configurar o SSO para o seu aplicativo, acesse a página [Configuração de SSO empresarial do Trello](https://trello.com/sso-configuration) para enviar à [equipe de suporte do Trello](mailto:support@trello.com) a **URL do Serviço de Logon Único SAML** e anexe o **Certificado (Base64)**.</span><span class="sxs-lookup"><span data-stu-id="17998-197">To get SSO configured for your application, go to [Trello enterprise SSO configuration](https://trello.com/sso-configuration) page to send [Trello support team](mailto:support@trello.com) the **SAML Single Sign-On Service URL** and attach the **Certificate (Base64)**.</span></span>

> [!TIP]
> <span data-ttu-id="17998-198">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="17998-198">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="17998-199">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="17998-199">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="17998-200">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="17998-200">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="17998-201">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="17998-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="17998-202">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="17998-202">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="17998-204">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="17998-204">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="17998-205">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="17998-205">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-trello-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="17998-207">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="17998-207">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-trello-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="17998-209">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="17998-209">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-trello-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="17998-211">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="17998-211">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-trello-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="17998-213">a.</span><span class="sxs-lookup"><span data-stu-id="17998-213">a.</span></span> <span data-ttu-id="17998-214">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="17998-214">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="17998-215">b.</span><span class="sxs-lookup"><span data-stu-id="17998-215">b.</span></span> <span data-ttu-id="17998-216">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="17998-216">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="17998-217">c.</span><span class="sxs-lookup"><span data-stu-id="17998-217">c.</span></span> <span data-ttu-id="17998-218">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="17998-218">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="17998-219">d.</span><span class="sxs-lookup"><span data-stu-id="17998-219">d.</span></span> <span data-ttu-id="17998-220">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="17998-220">Click **Create**.</span></span>
 
### <a name="creating-a-trello-test-user"></a><span data-ttu-id="17998-221">Criando um usuário de teste do Trello</span><span class="sxs-lookup"><span data-stu-id="17998-221">Creating a Trello test user</span></span>

<span data-ttu-id="17998-222">Nesta seção, você cria um usuário chamado Brenda Fernandes no Trello.</span><span class="sxs-lookup"><span data-stu-id="17998-222">In this section, you create a user called Britta Simon in Trello.</span></span> <span data-ttu-id="17998-223">Nesta seção, você cria um usuário chamado Brenda Fernandes no Trello.</span><span class="sxs-lookup"><span data-stu-id="17998-223">In this section, you create a user called Britta Simon in Trello.</span></span> <span data-ttu-id="17998-224">O Trello dá suporte ao provisionamento Just-In-Time e uma nova conta é criada na primeira vez em que você entra por meio do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="17998-224">Trello supports just-in-time provisioning and a new account is created the first time you sign in from Azure AD.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="17998-225">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="17998-225">Assigning the Azure AD test user</span></span>

<span data-ttu-id="17998-226">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo acesso ao Trello.</span><span class="sxs-lookup"><span data-stu-id="17998-226">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Trello.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="17998-228">**Para atribuir Brenda Fernandes ao Trello, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="17998-228">**To assign Britta Simon to Trello, perform the following steps:**</span></span>

1. <span data-ttu-id="17998-229">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="17998-229">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="17998-231">Na lista de aplicativos, selecione **Trello**.</span><span class="sxs-lookup"><span data-stu-id="17998-231">In the applications list, select **Trello**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-trello-tutorial/tutorial_trello_app.png) 

3. <span data-ttu-id="17998-233">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="17998-233">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="17998-235">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="17998-235">Click **Add** button.</span></span> <span data-ttu-id="17998-236">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="17998-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="17998-238">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="17998-238">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="17998-239">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="17998-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="17998-240">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="17998-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="17998-241">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="17998-241">Testing single sign-on</span></span>

<span data-ttu-id="17998-242">O objetivo desta seção é testar sua configuração de SSO do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="17998-242">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="17998-243">Ao clicar no bloco do Trello no Painel de Acesso, você deverá ser conectado automaticamente ao seu aplicativo Trello.</span><span class="sxs-lookup"><span data-stu-id="17998-243">When you click the Trello tile in the Access Panel, you should get automatically signed-on to your Trello application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="17998-244">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="17998-244">Additional resources</span></span>

* [<span data-ttu-id="17998-245">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="17998-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="17998-246">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="17998-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-trello-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-trello-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-trello-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-trello-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-trello-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-trello-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-trello-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-trello-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-trello-tutorial/tutorial_general_203.png

