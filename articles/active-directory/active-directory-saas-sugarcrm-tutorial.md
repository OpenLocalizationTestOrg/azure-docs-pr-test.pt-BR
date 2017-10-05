---
title: "Tutorial: integração do Azure Active Directory ao Sugar CRM | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Sugar CRM."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3331b9fc-ebc0-4a3a-9f7b-bf20ee35d180
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: jeedes
ms.openlocfilehash: c27aef24e859522b8001ecb747906abdca14d87a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sugar-crm"></a><span data-ttu-id="3bbfa-103">Tutorial: integração do Azure Active Directory ao Sugar CRM</span><span class="sxs-lookup"><span data-stu-id="3bbfa-103">Tutorial: Azure Active Directory integration with Sugar CRM</span></span>

<span data-ttu-id="3bbfa-104">Neste tutorial, você aprenderá a integrar o Sugar CRM ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="3bbfa-104">In this tutorial, you learn how to integrate Sugar CRM with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3bbfa-105">A integração do Sugar CRM ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="3bbfa-105">Integrating Sugar CRM with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3bbfa-106">No Azure AD, é possível controlar quem tem acesso ao Sugar CRM</span><span class="sxs-lookup"><span data-stu-id="3bbfa-106">You can control in Azure AD who has access to Sugar CRM</span></span>
- <span data-ttu-id="3bbfa-107">Você pode permitir que os usuários façam logon automaticamente no Sugar CRM (logon único) com as respectivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="3bbfa-107">You can enable your users to automatically get signed-on to Sugar CRM (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3bbfa-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="3bbfa-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="3bbfa-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3bbfa-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3bbfa-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="3bbfa-110">Prerequisites</span></span>

<span data-ttu-id="3bbfa-111">Para configurar a integração do Azure AD ao Sugar CRM, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="3bbfa-111">To configure Azure AD integration with Sugar CRM, you need the following items:</span></span>

- <span data-ttu-id="3bbfa-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3bbfa-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3bbfa-113">Uma assinatura do Sugar CRM habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="3bbfa-113">A Sugar CRM single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3bbfa-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="3bbfa-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3bbfa-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="3bbfa-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3bbfa-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="3bbfa-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3bbfa-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3bbfa-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3bbfa-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="3bbfa-118">Scenario description</span></span>
<span data-ttu-id="3bbfa-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="3bbfa-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3bbfa-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="3bbfa-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3bbfa-121">Adicionar o Sugar CRM da galeria</span><span class="sxs-lookup"><span data-stu-id="3bbfa-121">Adding Sugar CRM from the gallery</span></span>
2. <span data-ttu-id="3bbfa-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3bbfa-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sugar-crm-from-the-gallery"></a><span data-ttu-id="3bbfa-123">Adicionar o Sugar CRM da galeria</span><span class="sxs-lookup"><span data-stu-id="3bbfa-123">Adding Sugar CRM from the gallery</span></span>
<span data-ttu-id="3bbfa-124">Para configurar a integração do Sugar CRM ao Azure AD, você precisará adicionar o Sugar CRM da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="3bbfa-124">To configure the integration of Sugar CRM into Azure AD, you need to add Sugar CRM from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3bbfa-125">**Para adicionar o Sugar CRM da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="3bbfa-125">**To add Sugar CRM from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3bbfa-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3bbfa-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3bbfa-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="3bbfa-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="3bbfa-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="3bbfa-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="3bbfa-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3bbfa-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="3bbfa-133">Na caixa de pesquisa, digite **SugarCRM**.</span><span class="sxs-lookup"><span data-stu-id="3bbfa-133">In the search box, type **Sugar CRM**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_search.png)

5. <span data-ttu-id="3bbfa-135">No painel de resultados, selecione **Sugar CRM** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3bbfa-135">In the results panel, select **Sugar CRM**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3bbfa-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3bbfa-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3bbfa-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Sugar CRM, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="3bbfa-138">In this section, you configure and test Azure AD single sign-on with Sugar CRM based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3bbfa-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Sugar CRM é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3bbfa-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Sugar CRM is to a user in Azure AD.</span></span> <span data-ttu-id="3bbfa-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado no Sugar CRM.</span><span class="sxs-lookup"><span data-stu-id="3bbfa-140">In other words, a link relationship between an Azure AD user and the related user in Sugar CRM needs to be established.</span></span>

<span data-ttu-id="3bbfa-141">No Sugar CRM, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="3bbfa-141">In Sugar CRM, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="3bbfa-142">Para configurar e testar o logon único do Azure AD com o Sugar CRM, você precisará concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="3bbfa-142">To configure and test Azure AD single sign-on with Sugar CRM, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3bbfa-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="3bbfa-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3bbfa-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="3bbfa-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3bbfa-145">**[Criar um usuário de teste do Sugar CRM](#creating-a-sugar-crm-test-user)** – para ter um equivalente de Brenda Fernandes no Sugar CRM que esteja vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3bbfa-145">**[Creating a Sugar CRM test user](#creating-a-sugar-crm-test-user)** - to have a counterpart of Britta Simon in Sugar CRM that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="3bbfa-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="3bbfa-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3bbfa-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="3bbfa-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3bbfa-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="3bbfa-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3bbfa-149">Nesta seção, você habilitará o logon único do Azure AD no Portal do Azure e configurará o logon único no aplicativo Sugar CRM.</span><span class="sxs-lookup"><span data-stu-id="3bbfa-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Sugar CRM application.</span></span>

<span data-ttu-id="3bbfa-150">**Para configurar o logon único do Azure AD com o Sugar CRM, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="3bbfa-150">**To configure Azure AD single sign-on with Sugar CRM, perform the following steps:**</span></span>

1. <span data-ttu-id="3bbfa-151">No Portal do Azure, na página de integração de aplicativos do **Sugar CRM**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="3bbfa-151">In the Azure portal, on the **Sugar CRM** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="3bbfa-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="3bbfa-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_samlbase.png)

3. <span data-ttu-id="3bbfa-155">Na seção **Domínio e URLs do Sugar CRM**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="3bbfa-155">On the **Sugar CRM Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_url.png)

    <span data-ttu-id="3bbfa-157">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão:</span><span class="sxs-lookup"><span data-stu-id="3bbfa-157">In the **Sign-on URL** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.sugarondemand.com` |
    | `https://<companyname>.trial.sugarcrm` |

    > [!NOTE] 
    > <span data-ttu-id="3bbfa-158">O valor não é real.</span><span class="sxs-lookup"><span data-stu-id="3bbfa-158">The value is not real.</span></span> <span data-ttu-id="3bbfa-159">Atualize o valor com a URL de Logon real.</span><span class="sxs-lookup"><span data-stu-id="3bbfa-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="3bbfa-160">Contate [equipe de suporte ao cliente do Sugar CRM](https://support.sugarcrm.com/) para obter o valor.</span><span class="sxs-lookup"><span data-stu-id="3bbfa-160">Contact [Sugar CRM Client support team](https://support.sugarcrm.com/) to get the value.</span></span> 
 
4. <span data-ttu-id="3bbfa-161">Na seção **Certificado de Autenticação SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado em seu computador.</span><span class="sxs-lookup"><span data-stu-id="3bbfa-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_certificate.png) 

5. <span data-ttu-id="3bbfa-163">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="3bbfa-163">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="3bbfa-165">Na seção **Configuração do Sugar CRM**, clique em **Configurar o Sugar CRM** para abrir a janela **Configurar o logon**.</span><span class="sxs-lookup"><span data-stu-id="3bbfa-165">On the **Sugar CRM Configuration** section, click **Configure Sugar CRM** to open **Configure sign-on** window.</span></span> <span data-ttu-id="3bbfa-166">Copie a **URL de Saída e a URL do Serviço de Logon Único SAML** da **seção Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="3bbfa-166">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_configure.png) 

7. <span data-ttu-id="3bbfa-168">Em outra janela do navegador da Web, faça logon em seu site de empresa do SugarCRM como um administrador.</span><span class="sxs-lookup"><span data-stu-id="3bbfa-168">In a different web browser window, log in to your Sugar CRM company site as an administrator.</span></span>

8. <span data-ttu-id="3bbfa-169">Vá para **Administrador**.</span><span class="sxs-lookup"><span data-stu-id="3bbfa-169">Go to **Admin**.</span></span>
   
    <span data-ttu-id="3bbfa-170">![Admin](./media/active-directory-saas-sugarcrm-tutorial/ic795888.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="3bbfa-170">![Admin](./media/active-directory-saas-sugarcrm-tutorial/ic795888.png "Admin")</span></span>

9. <span data-ttu-id="3bbfa-171">Na seção **Administração**, clique em **Gerenciamento de Senhas**.</span><span class="sxs-lookup"><span data-stu-id="3bbfa-171">In the **Administration** section, click **Password Management**.</span></span>
   
    <span data-ttu-id="3bbfa-172">![Administração](./media/active-directory-saas-sugarcrm-tutorial/ic795889.png "Administração")</span><span class="sxs-lookup"><span data-stu-id="3bbfa-172">![Administration](./media/active-directory-saas-sugarcrm-tutorial/ic795889.png "Administration")</span></span>

10. <span data-ttu-id="3bbfa-173">Selecione **Habilitar Autenticação SAML**.</span><span class="sxs-lookup"><span data-stu-id="3bbfa-173">Select **Enable SAML Authentication**.</span></span>
   
    <span data-ttu-id="3bbfa-174">![Administração](./media/active-directory-saas-sugarcrm-tutorial/ic795890.png "Administração")</span><span class="sxs-lookup"><span data-stu-id="3bbfa-174">![Administration](./media/active-directory-saas-sugarcrm-tutorial/ic795890.png "Administration")</span></span>

11. <span data-ttu-id="3bbfa-175">Na seção **Autenticação SAML** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="3bbfa-175">In the **SAML Authentication** section, perform the following steps:</span></span>
   
    <span data-ttu-id="3bbfa-176">![Autenticação SAML](./media/active-directory-saas-sugarcrm-tutorial/ic795891.png "Autenticação SAML")</span><span class="sxs-lookup"><span data-stu-id="3bbfa-176">![SAML Authentication](./media/active-directory-saas-sugarcrm-tutorial/ic795891.png "SAML Authentication")</span></span>  
 
    <span data-ttu-id="3bbfa-177">a.</span><span class="sxs-lookup"><span data-stu-id="3bbfa-177">a.</span></span> <span data-ttu-id="3bbfa-178">Na caixa de texto **URL de Logon**, cole o valor da **URL do Serviço de Logon Único SAML** copiado do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="3bbfa-178">In the **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="3bbfa-179">b.</span><span class="sxs-lookup"><span data-stu-id="3bbfa-179">b.</span></span> <span data-ttu-id="3bbfa-180">Na caixa de texto **URL de SLO**, cole o valor da **URL de Saída** copiado do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="3bbfa-180">In the **SLO URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="3bbfa-181">c.</span><span class="sxs-lookup"><span data-stu-id="3bbfa-181">c.</span></span> <span data-ttu-id="3bbfa-182">Abra seu certificado codificado em Base 64 no bloco de notas, copie o conteúdo dele na área de transferência e cole todo o Certificado na caixa de texto **Certificado X.509** .</span><span class="sxs-lookup"><span data-stu-id="3bbfa-182">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste the entire Certificate into **X.509 Certificate** textbox.</span></span>
  
    <span data-ttu-id="3bbfa-183">d.</span><span class="sxs-lookup"><span data-stu-id="3bbfa-183">d.</span></span> <span data-ttu-id="3bbfa-184">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="3bbfa-184">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="3bbfa-185">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="3bbfa-185">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="3bbfa-186">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="3bbfa-186">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="3bbfa-187">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3bbfa-187">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3bbfa-188">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3bbfa-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="3bbfa-189">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="3bbfa-189">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="3bbfa-191">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="3bbfa-191">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3bbfa-192">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3bbfa-192">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sugarcrm-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3bbfa-194">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="3bbfa-194">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sugarcrm-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3bbfa-196">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3bbfa-196">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sugarcrm-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3bbfa-198">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="3bbfa-198">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sugarcrm-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3bbfa-200">a.</span><span class="sxs-lookup"><span data-stu-id="3bbfa-200">a.</span></span> <span data-ttu-id="3bbfa-201">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="3bbfa-201">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3bbfa-202">b.</span><span class="sxs-lookup"><span data-stu-id="3bbfa-202">b.</span></span> <span data-ttu-id="3bbfa-203">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="3bbfa-203">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3bbfa-204">c.</span><span class="sxs-lookup"><span data-stu-id="3bbfa-204">c.</span></span> <span data-ttu-id="3bbfa-205">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="3bbfa-205">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="3bbfa-206">d.</span><span class="sxs-lookup"><span data-stu-id="3bbfa-206">d.</span></span> <span data-ttu-id="3bbfa-207">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="3bbfa-207">Click **Create**.</span></span>
 
### <a name="creating-a-sugar-crm-test-user"></a><span data-ttu-id="3bbfa-208">Criar um usuário de teste do Sugar CRM</span><span class="sxs-lookup"><span data-stu-id="3bbfa-208">Creating a Sugar CRM test user</span></span>

<span data-ttu-id="3bbfa-209">Para permitir que os usuários do Azure AD façam logon no SugarCRM, eles devem estar provisionados no SugarCRM.</span><span class="sxs-lookup"><span data-stu-id="3bbfa-209">In order to enable Azure AD users to log in to Sugar CRM, they must be provisioned to Sugar CRM.</span></span>

<span data-ttu-id="3bbfa-210">No caso do SugarCRM, o provisionamento será uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="3bbfa-210">In the case of Sugar CRM, provisioning is a manual task.</span></span>

<span data-ttu-id="3bbfa-211">**Para provisionar uma conta de usuário, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="3bbfa-211">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="3bbfa-212">Faça logon em seu site de empresa do **SugarCRM** como administrador.</span><span class="sxs-lookup"><span data-stu-id="3bbfa-212">Log in to your **Sugar CRM** company site as administrator.</span></span>

2. <span data-ttu-id="3bbfa-213">Vá para **Administrador**.</span><span class="sxs-lookup"><span data-stu-id="3bbfa-213">Go to **Admin**.</span></span>
   
    <span data-ttu-id="3bbfa-214">![Admin](./media/active-directory-saas-sugarcrm-tutorial/ic795888.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="3bbfa-214">![Admin](./media/active-directory-saas-sugarcrm-tutorial/ic795888.png "Admin")</span></span>

3. <span data-ttu-id="3bbfa-215">Na seção **Administração**, clique em **Gerenciamento de Usuários**.</span><span class="sxs-lookup"><span data-stu-id="3bbfa-215">In the **Administration** section, click **User Management**.</span></span>
   
    <span data-ttu-id="3bbfa-216">![Administração](./media/active-directory-saas-sugarcrm-tutorial/ic795893.png "Administração")</span><span class="sxs-lookup"><span data-stu-id="3bbfa-216">![Administration](./media/active-directory-saas-sugarcrm-tutorial/ic795893.png "Administration")</span></span>

4. <span data-ttu-id="3bbfa-217">Vá para **Usuários \> Criar Novo Usuário**.</span><span class="sxs-lookup"><span data-stu-id="3bbfa-217">Go to **Users \> Create New User**.</span></span>
   
    <span data-ttu-id="3bbfa-218">![Criar Novo Usuário](./media/active-directory-saas-sugarcrm-tutorial/ic795894.png "Criar Novo Usuário")</span><span class="sxs-lookup"><span data-stu-id="3bbfa-218">![Create New User](./media/active-directory-saas-sugarcrm-tutorial/ic795894.png "Create New User")</span></span>

5. <span data-ttu-id="3bbfa-219">Na guia **Perfil do Usuário** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="3bbfa-219">On the **User Profile** tab, perform the following steps:</span></span>
   
    <span data-ttu-id="3bbfa-220">![Novo Usuário](./media/active-directory-saas-sugarcrm-tutorial/ic795895.png "Novo Usuário")</span><span class="sxs-lookup"><span data-stu-id="3bbfa-220">![New User](./media/active-directory-saas-sugarcrm-tutorial/ic795895.png "New User")</span></span>

    <span data-ttu-id="3bbfa-221">a.</span><span class="sxs-lookup"><span data-stu-id="3bbfa-221">a.</span></span> <span data-ttu-id="3bbfa-222">Digite o **nome de usuário**, o **sobrenome** e o **endereço de email** de um usuário válido do Azure Active Directory nas caixas de texto relacionadas.</span><span class="sxs-lookup"><span data-stu-id="3bbfa-222">Type the **user name**, **last name**, and **email address** of a valid Azure Active Directory user into the related textboxes.</span></span>
  
6. <span data-ttu-id="3bbfa-223">Para **Status**, selecione **Ativo**.</span><span class="sxs-lookup"><span data-stu-id="3bbfa-223">As **Status**, select **Active**.</span></span>

7. <span data-ttu-id="3bbfa-224">Na guia Senha, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="3bbfa-224">On the Password tab, perform the following steps:</span></span>
   
    <span data-ttu-id="3bbfa-225">![Novo Usuário](./media/active-directory-saas-sugarcrm-tutorial/ic795896.png "Novo Usuário")</span><span class="sxs-lookup"><span data-stu-id="3bbfa-225">![New User](./media/active-directory-saas-sugarcrm-tutorial/ic795896.png "New User")</span></span>

    <span data-ttu-id="3bbfa-226">a.</span><span class="sxs-lookup"><span data-stu-id="3bbfa-226">a.</span></span> <span data-ttu-id="3bbfa-227">Digite a senha na caixa de texto relacionada.</span><span class="sxs-lookup"><span data-stu-id="3bbfa-227">Type the password into the related textbox.</span></span>

    <span data-ttu-id="3bbfa-228">b.</span><span class="sxs-lookup"><span data-stu-id="3bbfa-228">b.</span></span> <span data-ttu-id="3bbfa-229">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="3bbfa-229">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="3bbfa-230">É possível usar qualquer outra ferramenta de criação da conta de usuário do SugarCRM ou as APIs fornecidas pelo SugarCRM para provisionar as contas de usuário do AAD.</span><span class="sxs-lookup"><span data-stu-id="3bbfa-230">You can use any other Sugar CRM user account creation tools or APIs provided by Sugar CRM to provision AAD user accounts.</span></span> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="3bbfa-231">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3bbfa-231">Assigning the Azure AD test user</span></span>

<span data-ttu-id="3bbfa-232">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao Sugar CRM.</span><span class="sxs-lookup"><span data-stu-id="3bbfa-232">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Sugar CRM.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="3bbfa-234">**Para atribuir Brenda Fernandes ao Sugar CRM, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="3bbfa-234">**To assign Britta Simon to Sugar CRM, perform the following steps:**</span></span>

1. <span data-ttu-id="3bbfa-235">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="3bbfa-235">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="3bbfa-237">Na lista de aplicativos, selecione **Sugar CRM**.</span><span class="sxs-lookup"><span data-stu-id="3bbfa-237">In the applications list, select **Sugar CRM**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_app.png) 

3. <span data-ttu-id="3bbfa-239">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="3bbfa-239">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="3bbfa-241">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="3bbfa-241">Click **Add** button.</span></span> <span data-ttu-id="3bbfa-242">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3bbfa-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="3bbfa-244">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="3bbfa-244">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="3bbfa-245">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3bbfa-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3bbfa-246">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3bbfa-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3bbfa-247">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="3bbfa-247">Testing single sign-on</span></span>

<span data-ttu-id="3bbfa-248">O objetivo desta seção é testar sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="3bbfa-248">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="3bbfa-249">Ao clicar no bloco do Sugar CRM no Painel de Acesso, você deverá ser conectado automaticamente ao aplicativo Sugar CRM.</span><span class="sxs-lookup"><span data-stu-id="3bbfa-249">When you click the Sugar CRM tile in the Access Panel, you should get automatically signed-on to your Sugar CRM application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3bbfa-250">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="3bbfa-250">Additional resources</span></span>

* [<span data-ttu-id="3bbfa-251">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="3bbfa-251">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3bbfa-252">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3bbfa-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_203.png

