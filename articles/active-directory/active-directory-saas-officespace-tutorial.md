---
title: "Tutorial: Integração do Azure Active Directory com o OfficeSpace Software | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e do OfficeSpace Software."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 95d8413f-db98-4e2c-8097-9142ef1af823
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: b53afb648b8a6057c32c782d857e34c06e152c67
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-officespace-software"></a><span data-ttu-id="b18dc-103">Tutorial: Integração do Active Directory do Azure com o OfficeSpace Software</span><span class="sxs-lookup"><span data-stu-id="b18dc-103">Tutorial: Azure Active Directory integration with OfficeSpace Software</span></span>

<span data-ttu-id="b18dc-104">Neste tutorial, você aprenderá como toointegrate OfficeSpace Software com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="b18dc-104">In this tutorial, you learn how toointegrate OfficeSpace Software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b18dc-105">Integração do OfficeSpace Software com o Azure AD oferece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="b18dc-105">Integrating OfficeSpace Software with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b18dc-106">Você pode controlar no AD do Azure que tenha acesso tooOfficeSpace Software.</span><span class="sxs-lookup"><span data-stu-id="b18dc-106">You can control in Azure AD who has access tooOfficeSpace Software.</span></span>
- <span data-ttu-id="b18dc-107">Você pode habilitar seu usuários tooautomatically get conectado tooOfficeSpace Software (logon único) com suas contas do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="b18dc-107">You can enable your users tooautomatically get signed-on tooOfficeSpace Software (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="b18dc-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b18dc-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="b18dc-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b18dc-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b18dc-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="b18dc-110">Prerequisites</span></span>

<span data-ttu-id="b18dc-111">tooconfigure integração do AD do Azure com o OfficeSpace Software, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="b18dc-111">tooconfigure Azure AD integration with OfficeSpace Software, you need hello following items:</span></span>

- <span data-ttu-id="b18dc-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="b18dc-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b18dc-113">Uma assinatura do OfficeSpace Software habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="b18dc-113">A OfficeSpace Software single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b18dc-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="b18dc-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b18dc-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="b18dc-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b18dc-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="b18dc-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b18dc-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b18dc-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b18dc-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="b18dc-118">Scenario description</span></span>
<span data-ttu-id="b18dc-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="b18dc-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b18dc-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="b18dc-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b18dc-121">Adicionando OfficeSpace Software da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="b18dc-121">Adding OfficeSpace Software from hello gallery</span></span>
2. <span data-ttu-id="b18dc-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="b18dc-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-officespace-software-from-hello-gallery"></a><span data-ttu-id="b18dc-123">Adicionando OfficeSpace Software da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="b18dc-123">Adding OfficeSpace Software from hello gallery</span></span>
<span data-ttu-id="b18dc-124">integração de saudação tooconfigure do OfficeSpace Software no AD do Azure, você precisa tooadd OfficeSpace Software na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="b18dc-124">tooconfigure hello integration of OfficeSpace Software into Azure AD, you need tooadd OfficeSpace Software from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b18dc-125">**tooadd OfficeSpace Software da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="b18dc-125">**tooadd OfficeSpace Software from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b18dc-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="b18dc-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botão de Active Directory do Azure Olá][1]

2. <span data-ttu-id="b18dc-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="b18dc-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b18dc-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="b18dc-129">Then go too**All applications**.</span></span>

    ![folha de aplicativos de empresa Olá][2]
    
3. <span data-ttu-id="b18dc-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b18dc-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Novo botão de aplicativo Hello][3]

4. <span data-ttu-id="b18dc-133">Na caixa de pesquisa hello, digite **OfficeSpace Software**, selecione **OfficeSpace Software** no painel de resultados e clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="b18dc-133">In hello search box, type **OfficeSpace Software**, select **OfficeSpace Software** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Lista de resultados do OfficeSpace Software em Olá](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="b18dc-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="b18dc-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="b18dc-136">Nesta seção, você configura e testa o logon único do Azure AD com o OfficeSpace Software, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="b18dc-136">In this section, you configure and test Azure AD single sign-on with OfficeSpace Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b18dc-137">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no OfficeSpace Software é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="b18dc-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in OfficeSpace Software is tooa user in Azure AD.</span></span> <span data-ttu-id="b18dc-138">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no OfficeSpace Software precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="b18dc-138">In other words, a link relationship between an Azure AD user and hello related user in OfficeSpace Software needs toobe established.</span></span>

<span data-ttu-id="b18dc-139">No OfficeSpace Software, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="b18dc-139">In OfficeSpace Software, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="b18dc-140">tooconfigure e teste de logon único do AD do Azure com o OfficeSpace Software, você precisa Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="b18dc-140">tooconfigure and test Azure AD single sign-on with OfficeSpace Software, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b18dc-141">**[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="b18dc-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b18dc-142">**[Criar um usuário de teste do AD do Azure](#create-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b18dc-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b18dc-143">**[Criar um usuário de teste do OfficeSpace Software](#create-a-officespace-software-test-user)**  -toohave um equivalente do Britta Simon no OfficeSpace Software que é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="b18dc-143">**[Create a OfficeSpace Software test user](#create-a-officespace-software-test-user)** - toohave a counterpart of Britta Simon in OfficeSpace Software that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="b18dc-144">**[Atribuir um usuário de teste de saudação do AD do Azure](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="b18dc-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b18dc-145">**[Testar o logon único](#test-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="b18dc-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="b18dc-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="b18dc-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="b18dc-147">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo OfficeSpace Software.</span><span class="sxs-lookup"><span data-stu-id="b18dc-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your OfficeSpace Software application.</span></span>

<span data-ttu-id="b18dc-148">**tooconfigure AD do Azure-logon único com o OfficeSpace Software, executar Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="b18dc-148">**tooconfigure Azure AD single sign-on with OfficeSpace Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="b18dc-149">Em Olá portal do Azure, Olá **OfficeSpace Software** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="b18dc-149">In hello Azure portal, on hello **OfficeSpace Software** application integration page, click **Single sign-on**.</span></span>

    ![Link Configurar logon único][4]

2. <span data-ttu-id="b18dc-151">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="b18dc-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_samlbase.png)

3. <span data-ttu-id="b18dc-153">Em Olá **OfficeSpace Software domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="b18dc-153">On hello **OfficeSpace Software Domain and URLs** section, perform hello following steps:</span></span>

    ![Informações de logon único de Domínio e URLs do OfficeSpace Software](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_url.png)

    <span data-ttu-id="b18dc-155">a.</span><span class="sxs-lookup"><span data-stu-id="b18dc-155">a.</span></span> <span data-ttu-id="b18dc-156">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<company name>.officespacesoftware.com/users/sign_in/saml`</span><span class="sxs-lookup"><span data-stu-id="b18dc-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company name>.officespacesoftware.com/users/sign_in/saml`</span></span>

    <span data-ttu-id="b18dc-157">b.</span><span class="sxs-lookup"><span data-stu-id="b18dc-157">b.</span></span> <span data-ttu-id="b18dc-158">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`<company name>.officespacesoftware.com`</span><span class="sxs-lookup"><span data-stu-id="b18dc-158">In hello **Identifier** textbox, type a URL using hello following pattern: `<company name>.officespacesoftware.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b18dc-159">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="b18dc-159">These values are not real.</span></span> <span data-ttu-id="b18dc-160">Atualizar esses valores com hello real URL de logon e o identificador.</span><span class="sxs-lookup"><span data-stu-id="b18dc-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="b18dc-161">Entre em contato com [equipe de suporte do OfficeSpace Software cliente](mailto:support@officespacesoftware.com) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="b18dc-161">Contact [OfficeSpace Software Client support team](mailto:support@officespacesoftware.com) tooget these values.</span></span> 

4. <span data-ttu-id="b18dc-162">Aplicativo OfficeSpace Software espera as asserções SAML de saudação em um formato específico.</span><span class="sxs-lookup"><span data-stu-id="b18dc-162">OfficeSpace Software application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="b18dc-163">Configure Olá declarações para esse aplicativo a seguir.</span><span class="sxs-lookup"><span data-stu-id="b18dc-163">Please configure hello following claims for this application.</span></span> <span data-ttu-id="b18dc-164">Você pode gerenciar os valores hello desses atributos de hello "**atributos de usuário**" na página de integração do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b18dc-164">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="b18dc-165">Olá captura de tela a seguir mostra um exemplo.</span><span class="sxs-lookup"><span data-stu-id="b18dc-165">hello following screenshot shows an example for this.</span></span>
    
    ![Configurar atributo](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_attribute.png)

5. <span data-ttu-id="b18dc-167">Em Olá **atributos de usuário** seção Olá **o logon único** caixa de diálogo, selecione **user.mail** como **identificador de usuário** e para cada linha mostrado na tabela de saudação abaixo, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="b18dc-167">In hello **User Attributes** section on hello **Single sign-on** dialog, select **user.mail**  as **User Identifier** and for each row shown in hello table below, perform hello following steps:</span></span>
    
    | <span data-ttu-id="b18dc-168">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="b18dc-168">Attribute Name</span></span> | <span data-ttu-id="b18dc-169">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="b18dc-169">Attribute Value</span></span> |
    | --- | --- |    
    | <span data-ttu-id="b18dc-170">email</span><span class="sxs-lookup"><span data-stu-id="b18dc-170">email</span></span> | <span data-ttu-id="b18dc-171">user.mail</span><span class="sxs-lookup"><span data-stu-id="b18dc-171">user.mail</span></span> |
    | <span data-ttu-id="b18dc-172">name</span><span class="sxs-lookup"><span data-stu-id="b18dc-172">name</span></span> | <span data-ttu-id="b18dc-173">user.displayname</span><span class="sxs-lookup"><span data-stu-id="b18dc-173">user.displayname</span></span> |
    | <span data-ttu-id="b18dc-174">first_name</span><span class="sxs-lookup"><span data-stu-id="b18dc-174">first_name</span></span> | <span data-ttu-id="b18dc-175">user.givenname</span><span class="sxs-lookup"><span data-stu-id="b18dc-175">user.givenname</span></span> |
    | <span data-ttu-id="b18dc-176">last_name</span><span class="sxs-lookup"><span data-stu-id="b18dc-176">last_name</span></span> | <span data-ttu-id="b18dc-177">user.surname</span><span class="sxs-lookup"><span data-stu-id="b18dc-177">user.surname</span></span> |

    <span data-ttu-id="b18dc-178">a.</span><span class="sxs-lookup"><span data-stu-id="b18dc-178">a.</span></span> <span data-ttu-id="b18dc-179">Clique em **Adicionar atributo** tooopen Olá **Adicionar atributo** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b18dc-179">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![<span data-ttu-id="b18dc-180">Configurar Adicionar</span><span class="sxs-lookup"><span data-stu-id="b18dc-180">Configure Add</span></span> ](./media/active-directory-saas-officespace-tutorial/tutorial_attribute_04.png)

    ![Configurar atributo](./media/active-directory-saas-officespace-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="b18dc-182">b.</span><span class="sxs-lookup"><span data-stu-id="b18dc-182">b.</span></span> <span data-ttu-id="b18dc-183">Em Olá **nome** caixa de texto, nome de atributo do tipo hello mostrado para aquela linha.</span><span class="sxs-lookup"><span data-stu-id="b18dc-183">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="b18dc-184">c.</span><span class="sxs-lookup"><span data-stu-id="b18dc-184">c.</span></span> <span data-ttu-id="b18dc-185">De saudação **valor** lista, o valor do atributo type Olá mostrado para aquela linha.</span><span class="sxs-lookup"><span data-stu-id="b18dc-185">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="b18dc-186">d.</span><span class="sxs-lookup"><span data-stu-id="b18dc-186">d.</span></span> <span data-ttu-id="b18dc-187">Clique em **Ok**</span><span class="sxs-lookup"><span data-stu-id="b18dc-187">Click **Ok**</span></span>
 
6. <span data-ttu-id="b18dc-188">Em Olá **o certificado de autenticação SAML** seção, Olá cópia **impressão digital** o valor de certificado hello.</span><span class="sxs-lookup"><span data-stu-id="b18dc-188">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of hello certificate.</span></span>

    ![link de download de certificado Olá](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_certificate.png) 

7. <span data-ttu-id="b18dc-190">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="b18dc-190">Click **Save** button.</span></span>

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-officespace-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="b18dc-192">Em Olá **OfficeSpace Software configuração** seção, clique em **configurar OfficeSpace Software** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="b18dc-192">On hello **OfficeSpace Software Configuration** section, click **Configure OfficeSpace Software** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="b18dc-193">Saudação de cópia **URL de logout e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="b18dc-193">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuração do OfficeSpace Software](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_configure.png) 

9. <span data-ttu-id="b18dc-195">Em outra janela do navegador da Web, faça logon no locatário do OfficeSpace Software como administrador.</span><span class="sxs-lookup"><span data-stu-id="b18dc-195">In a different web browser window, log into your OfficeSpace Software tenant as an administrator.</span></span>

10. <span data-ttu-id="b18dc-196">Vá muito**configurações** e clique em **conectores**.</span><span class="sxs-lookup"><span data-stu-id="b18dc-196">Go too**Settings** and click **Connectors**.</span></span>

    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_002.png)

11. <span data-ttu-id="b18dc-198">Clique em **Autenticação SAML**.</span><span class="sxs-lookup"><span data-stu-id="b18dc-198">Click **SAML Authentication**.</span></span>

    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_003.png)

12. <span data-ttu-id="b18dc-200">Em Olá **autenticação SAML** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="b18dc-200">In hello **SAML Authentication** section, perform hello following steps:</span></span>

    ![Configurar o logon único no lado do aplicativo](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_004.png)

    <span data-ttu-id="b18dc-202">a.</span><span class="sxs-lookup"><span data-stu-id="b18dc-202">a.</span></span> <span data-ttu-id="b18dc-203">Em Olá **url de Logout do provedor** caixa de texto valor Olá colar **URL de logout** que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b18dc-203">In hello **Logout provider url** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="b18dc-204">b.</span><span class="sxs-lookup"><span data-stu-id="b18dc-204">b.</span></span> <span data-ttu-id="b18dc-205">Em Olá **url de destino de idp cliente** caixa de texto valor Olá colar **Single Sign-On URL do serviço SAML** que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b18dc-205">In hello **Client idp target url** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="b18dc-206">c.</span><span class="sxs-lookup"><span data-stu-id="b18dc-206">c.</span></span> <span data-ttu-id="b18dc-207">Saudação de colar **impressão digital** valor que você copiou do portal do Azure, na Olá **impressão digital do certificado IDP cliente** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="b18dc-207">Paste hello **Thumbprint** value which you have copied from Azure portal, into hello **Client IDP certificate fingerprint** textbox.</span></span> 

    <span data-ttu-id="b18dc-208">d.</span><span class="sxs-lookup"><span data-stu-id="b18dc-208">d.</span></span> <span data-ttu-id="b18dc-209">Clique em **Salvar Configurações**.</span><span class="sxs-lookup"><span data-stu-id="b18dc-209">Click **Save Settings**.</span></span>


> [!TIP]
> <span data-ttu-id="b18dc-210">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="b18dc-210">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="b18dc-211">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="b18dc-211">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="b18dc-212">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b18dc-212">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="b18dc-213">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="b18dc-213">Create an Azure AD test user</span></span>

<span data-ttu-id="b18dc-214">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b18dc-214">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Criar um usuário de teste do Azure AD][100]

<span data-ttu-id="b18dc-216">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="b18dc-216">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b18dc-217">No hello portal do Azure, no painel esquerdo do hello, clique em Olá **Active Directory do Azure** botão.</span><span class="sxs-lookup"><span data-stu-id="b18dc-217">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![botão de Active Directory do Azure Olá](./media/active-directory-saas-officespace-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="b18dc-219">lista de saudação toodisplay de usuários, vá muito**usuários e grupos**e, em seguida, clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="b18dc-219">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Olá "Usuários e grupos" e "Todos os usuários" links](./media/active-directory-saas-officespace-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="b18dc-221">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação do hello **todos os usuários** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b18dc-221">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![botão Adicionar de saudação](./media/active-directory-saas-officespace-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="b18dc-223">Em Olá **usuário** caixa de diálogo caixa, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="b18dc-223">In hello **User** dialog box, perform hello following steps:</span></span>

    ![caixa de diálogo de usuário Olá](./media/active-directory-saas-officespace-tutorial/create_aaduser_04.png)

    <span data-ttu-id="b18dc-225">a.</span><span class="sxs-lookup"><span data-stu-id="b18dc-225">a.</span></span> <span data-ttu-id="b18dc-226">Em Olá **nome** , digite **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b18dc-226">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b18dc-227">b.</span><span class="sxs-lookup"><span data-stu-id="b18dc-227">b.</span></span> <span data-ttu-id="b18dc-228">Em Olá **nome de usuário** caixa tipo hello endereço de email do usuário Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b18dc-228">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="b18dc-229">c.</span><span class="sxs-lookup"><span data-stu-id="b18dc-229">c.</span></span> <span data-ttu-id="b18dc-230">Selecione Olá **Mostrar senha** caixa de seleção e anote o valor de saudação que é exibido no hello **senha** caixa.</span><span class="sxs-lookup"><span data-stu-id="b18dc-230">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="b18dc-231">d.</span><span class="sxs-lookup"><span data-stu-id="b18dc-231">d.</span></span> <span data-ttu-id="b18dc-232">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="b18dc-232">Click **Create**.</span></span>
 
### <a name="create-a-officespace-software-test-user"></a><span data-ttu-id="b18dc-233">Criar um usuário de teste do OfficeSpace Software</span><span class="sxs-lookup"><span data-stu-id="b18dc-233">Create a OfficeSpace Software test user</span></span>

<span data-ttu-id="b18dc-234">Olá o objetivo desta seção é toocreate um usuário chamado Britta Simon no OfficeSpace Software.</span><span class="sxs-lookup"><span data-stu-id="b18dc-234">hello objective of this section is toocreate a user called Britta Simon in OfficeSpace Software.</span></span> <span data-ttu-id="b18dc-235">O OfficeSpace Software dá suporte ao provisionamento Just-In-Time, que está habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="b18dc-235">OfficeSpace Software supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="b18dc-236">Não há itens de ação para você nesta seção.</span><span class="sxs-lookup"><span data-stu-id="b18dc-236">There is no action item for you in this section.</span></span> <span data-ttu-id="b18dc-237">Se ele ainda não existir, um novo usuário será criado durante uma tentativa tooaccess OfficeSpace Software.</span><span class="sxs-lookup"><span data-stu-id="b18dc-237">A new user will be created during an attempt tooaccess OfficeSpace Software if it doesn't exist yet.</span></span>

> [!NOTE]
> <span data-ttu-id="b18dc-238">Se você precisar toocreate um usuário manualmente, será necessário tooContact [equipe de suporte do OfficeSpace Software](mailto:support@officespacesoftware.com).</span><span class="sxs-lookup"><span data-stu-id="b18dc-238">If you need toocreate an user manually, you need tooContact [OfficeSpace Software support team](mailto:support@officespacesoftware.com).</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="b18dc-239">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="b18dc-239">Assign hello Azure AD test user</span></span>

<span data-ttu-id="b18dc-240">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooOfficeSpace Software.</span><span class="sxs-lookup"><span data-stu-id="b18dc-240">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooOfficeSpace Software.</span></span>

![Atribuir função de usuário Olá][200] 

<span data-ttu-id="b18dc-242">**tooassign Britta Simon tooOfficeSpace Software, executar Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="b18dc-242">**tooassign Britta Simon tooOfficeSpace Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="b18dc-243">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="b18dc-243">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="b18dc-245">Na lista de aplicativos hello, selecione **OfficeSpace Software**.</span><span class="sxs-lookup"><span data-stu-id="b18dc-245">In hello applications list, select **OfficeSpace Software**.</span></span>

    ![Olá link OfficeSpace Software na lista de aplicativos Olá](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_app.png)  

3. <span data-ttu-id="b18dc-247">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="b18dc-247">In hello menu on hello left, click **Users and groups**.</span></span>

    ![link de "Usuários e grupos" Hello][202]

4. <span data-ttu-id="b18dc-249">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="b18dc-249">Click **Add** button.</span></span> <span data-ttu-id="b18dc-250">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b18dc-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Painel de atribuição adicionar Olá][203]

5. <span data-ttu-id="b18dc-252">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="b18dc-252">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b18dc-253">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b18dc-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b18dc-254">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b18dc-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="b18dc-255">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="b18dc-255">Test single sign-on</span></span>

<span data-ttu-id="b18dc-256">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="b18dc-256">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="b18dc-257">Quando você clica em Olá lado a lado no painel de acesso de saudação OfficeSpace Software, você deve obter tooyour automaticamente conectado no aplicativo OfficeSpace Software.</span><span class="sxs-lookup"><span data-stu-id="b18dc-257">When you click hello OfficeSpace Software tile in hello Access Panel, you should get automatically signed-on tooyour OfficeSpace Software application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b18dc-258">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="b18dc-258">Additional resources</span></span>

* [<span data-ttu-id="b18dc-259">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="b18dc-259">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b18dc-260">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b18dc-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_203.png

