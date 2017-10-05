---
title: "Tutorial: integração do Azure Active Directory ao Evidence.com | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Active Directory do Azure e o Evidence.com."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: f9a7cb7c-ff67-40dc-872c-1fa35f9dd03b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: a9c474cfc648fc8a306d736c89a4813d82c133ea
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-evidencecom"></a><span data-ttu-id="5fc91-103">Tutorial: Integração do Active Directory do Azure ao Evidence.com</span><span class="sxs-lookup"><span data-stu-id="5fc91-103">Tutorial: Azure Active Directory integration with Evidence.com</span></span>

<span data-ttu-id="5fc91-104">Neste tutorial, você aprenderá a integrar o Evidence.com ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="5fc91-104">In this tutorial, you learn how to integrate Evidence.com with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5fc91-105">A integração do Evidence.com ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="5fc91-105">Integrating Evidence.com with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="5fc91-106">No Azure AD, é possível controlar quem tem acesso ao Evidence.com.</span><span class="sxs-lookup"><span data-stu-id="5fc91-106">You can control in Azure AD who has access to Evidence.com.</span></span>
- <span data-ttu-id="5fc91-107">Você pode permitir que os usuários façam logon automaticamente no Evidence.com (Logon Único) com as respectivas contas do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5fc91-107">You can enable your users to automatically get signed-on to Evidence.com (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="5fc91-108">Você pode gerenciar suas contas em um único local central – o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="5fc91-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="5fc91-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5fc91-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5fc91-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="5fc91-110">Prerequisites</span></span>

<span data-ttu-id="5fc91-111">Para configurar a integração do Azure AD com o Evidence.com, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="5fc91-111">To configure Azure AD integration with Evidence.com, you need the following items:</span></span>

- <span data-ttu-id="5fc91-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="5fc91-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5fc91-113">Uma assinatura do Evidence.com habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="5fc91-113">A Evidence.com single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5fc91-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="5fc91-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5fc91-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="5fc91-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5fc91-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="5fc91-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5fc91-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5fc91-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5fc91-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="5fc91-118">Scenario description</span></span>
<span data-ttu-id="5fc91-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="5fc91-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5fc91-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="5fc91-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5fc91-121">Adicionar o Evidence.com da galeria</span><span class="sxs-lookup"><span data-stu-id="5fc91-121">Adding Evidence.com from the gallery</span></span>
2. <span data-ttu-id="5fc91-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="5fc91-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-evidencecom-from-the-gallery"></a><span data-ttu-id="5fc91-123">Adicionar o Evidence.com da galeria</span><span class="sxs-lookup"><span data-stu-id="5fc91-123">Adding Evidence.com from the gallery</span></span>
<span data-ttu-id="5fc91-124">Para configurar a integração do Evidence.com ao Azure AD, é necessário adicionar o Evidence.com da galeria à lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="5fc91-124">To configure the integration of Evidence.com into Azure AD, you need to add Evidence.com from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="5fc91-125">**Para adicionar o Evidence.com da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="5fc91-125">**To add Evidence.com from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="5fc91-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5fc91-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![O botão Azure Active Directory][1]

2. <span data-ttu-id="5fc91-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="5fc91-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="5fc91-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="5fc91-129">Then go to **All applications**.</span></span>

    ![A folha Aplicativos empresariais][2]
    
3. <span data-ttu-id="5fc91-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5fc91-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![O botão Novo aplicativo][3]

4. <span data-ttu-id="5fc91-133">Na caixa de pesquisa, digite **Evidence.com**, selecione **Evidence.com** no painel de resultados e, em seguida, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5fc91-133">In the search box, type **Evidence.com**, select **Evidence.com** from result panel then click **Add** button to add the application.</span></span>

    ![Evidence.com na lista de resultados](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="5fc91-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="5fc91-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="5fc91-136">Nesta seção, você configurará e testará o logon único do Azure AD com o Evidence.com, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="5fc91-136">In this section, you configure and test Azure AD single sign-on with Evidence.com based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5fc91-137">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Evidence.com é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5fc91-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Evidence.com is to a user in Azure AD.</span></span> <span data-ttu-id="5fc91-138">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado no Evidence.com.</span><span class="sxs-lookup"><span data-stu-id="5fc91-138">In other words, a link relationship between an Azure AD user and the related user in Evidence.com needs to be established.</span></span>

<span data-ttu-id="5fc91-139">No Evidence.com, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="5fc91-139">In Evidence.com, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="5fc91-140">Para configurar e testar o logon único do Azure AD com o Evidence.com, você precisará concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="5fc91-140">To configure and test Azure AD single sign-on with Evidence.com, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5fc91-141">**[Configurar o logon único do Azure AD](#configure-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="5fc91-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="5fc91-142">**[Criar um usuário de teste do Azure AD](#create-an-azure-ad-test-user)** – para testar o logon único do Azure AD com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="5fc91-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5fc91-143">**[Criar um usuário de teste do Evidence.com](#create-a-evidencecom-test-user)** – para ter um equivalente de Brenda Fernandes no Evidence.com vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5fc91-143">**[Create a Evidence.com test user](#create-a-evidencecom-test-user)** - to have a counterpart of Britta Simon in Evidence.com that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="5fc91-144">**[Atribuir o usuário de teste do Azure AD](#assign-the-azure-ad-test-user)** – para permitir que Brenda Fernandes use o logon único do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5fc91-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5fc91-145">**[Teste o logon único](#test-single-sign-on)** – para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="5fc91-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="5fc91-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="5fc91-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="5fc91-147">Nesta seção, você habilitará o logon único do Azure AD no Portal do Azure e configurará o logon único no aplicativo Evidence.com.</span><span class="sxs-lookup"><span data-stu-id="5fc91-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Evidence.com application.</span></span>

<span data-ttu-id="5fc91-148">**Para configurar o logon único do Azure AD com o Evidence.com, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="5fc91-148">**To configure Azure AD single sign-on with Evidence.com, perform the following steps:**</span></span>

1. <span data-ttu-id="5fc91-149">No Portal do Azure, na página de integração de aplicativos do **Evidence.com**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="5fc91-149">In the Azure portal, on the **Evidence.com** application integration page, click **Single sign-on**.</span></span>

    ![Link Configurar logon único][4]

2. <span data-ttu-id="5fc91-151">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="5fc91-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_samlbase.png)

3. <span data-ttu-id="5fc91-153">Na seção **Domínio e URLs do Evidence.com**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="5fc91-153">On the **Evidence.com Domain and URLs** section, perform the following steps:</span></span>

    ![Informações de logon único de Domínio e URLs do Evidence.com](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_url.png)

    <span data-ttu-id="5fc91-155">a.</span><span class="sxs-lookup"><span data-stu-id="5fc91-155">a.</span></span> <span data-ttu-id="5fc91-156">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<yourtenant>.evidence.com`</span><span class="sxs-lookup"><span data-stu-id="5fc91-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<yourtenant>.evidence.com`</span></span>

    <span data-ttu-id="5fc91-157">b.</span><span class="sxs-lookup"><span data-stu-id="5fc91-157">b.</span></span> <span data-ttu-id="5fc91-158">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<yourtenant>.evidence.com`</span><span class="sxs-lookup"><span data-stu-id="5fc91-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<yourtenant>.evidence.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5fc91-159">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="5fc91-159">These values are not real.</span></span> <span data-ttu-id="5fc91-160">Atualize esses valores com a URL de Entrada e o Identificador reais.</span><span class="sxs-lookup"><span data-stu-id="5fc91-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="5fc91-161">Contate a [equipe de suporte ao cliente do Evidence.com](https://communities.taser.com/support/SupportContactUs?typ=LE) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="5fc91-161">Contact [Evidence.com Client support team](https://communities.taser.com/support/SupportContactUs?typ=LE) to get these values.</span></span> 

4. <span data-ttu-id="5fc91-162">Na seção **Certificado de Autenticação do SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado no computador.</span><span class="sxs-lookup"><span data-stu-id="5fc91-162">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![O link de download do Certificado](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_certificate.png) 

5. <span data-ttu-id="5fc91-164">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="5fc91-164">Click **Save** button.</span></span>

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-evidence-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5fc91-166">Na seção **Configuração do Evidence.com**, clique em **Configurar o Evidence.com** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="5fc91-166">On the **Evidence.com Configuration** section, click **Configure Evidence.com** to open **Configure sign-on** window.</span></span> <span data-ttu-id="5fc91-167">Copie a **URL de saída, a ID da Entidade SAML e a URL do Serviço de Logon Único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="5fc91-167">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configuração do Evidence.com](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_configure.png) 

7. <span data-ttu-id="5fc91-169">Em uma janela separada do navegador da Web, faça logon como administrador em seu locatário do Evidence.com e navegue até a guia **Administrador**</span><span class="sxs-lookup"><span data-stu-id="5fc91-169">In a separate web browser window, login to your Evidence.com tenant as an administrator and navigate to **Admin** Tab</span></span>

8. <span data-ttu-id="5fc91-170">Clique em **Logon Único de Agência**</span><span class="sxs-lookup"><span data-stu-id="5fc91-170">Click on **Agency Single Sign On**</span></span>

9. <span data-ttu-id="5fc91-171">Escolha **Logon Único Baseado em SAML**</span><span class="sxs-lookup"><span data-stu-id="5fc91-171">Select **SAML Based Single Sign On**</span></span>

10. <span data-ttu-id="5fc91-172">Copie os valores de **ID da Entidade do SAML**, **URL do Serviço de Logon Único do SAML** e **URL de Saída** mostrados no Portal do Azure para os campos correspondentes no Evidence.com.</span><span class="sxs-lookup"><span data-stu-id="5fc91-172">Copy the **SAML Entity ID**, **SAML Single Sign-On Service URL** and **Sign-Out URL** values shown in the Azure portal and to the corresponding fields in Evidence.com.</span></span>

11. <span data-ttu-id="5fc91-173">Abra o arquivo de Certificado (Base64) baixado no bloco de notas, copie o conteúdo dele para a área de transferência e, depois, cole-o na caixa **Certificado de Segurança**.</span><span class="sxs-lookup"><span data-stu-id="5fc91-173">Open your downloaded Certificate(Base64) file in notepad, copy the content of it into your clipboard, and then paste it to the **Security Certificate** box.</span></span> 

12. <span data-ttu-id="5fc91-174">Salve a configuração no Evidence.com.</span><span class="sxs-lookup"><span data-stu-id="5fc91-174">Save the configuration in Evidence.com.</span></span>

> [!TIP]
> <span data-ttu-id="5fc91-175">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="5fc91-175">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="5fc91-176">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="5fc91-176">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="5fc91-177">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5fc91-177">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="5fc91-178">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="5fc91-178">Create an Azure AD test user</span></span>

<span data-ttu-id="5fc91-179">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="5fc91-179">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Criar um usuário de teste do Azure AD][100]

<span data-ttu-id="5fc91-181">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="5fc91-181">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5fc91-182">No portal do Azure, no painel esquerdo, clique no botão **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5fc91-182">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![O botão Azure Active Directory](./media/active-directory-saas-evidence-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="5fc91-184">Para exibir a lista de usuários, acesse **Usuários e grupos** e, depois, clique em **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="5fc91-184">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Os links “Usuários e grupos” e “Todos os usuários”](./media/active-directory-saas-evidence-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="5fc91-186">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo **Todos os Usuários**.</span><span class="sxs-lookup"><span data-stu-id="5fc91-186">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![O botão Adicionar](./media/active-directory-saas-evidence-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="5fc91-188">Na caixa de diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="5fc91-188">In the **User** dialog box, perform the following steps:</span></span>

    ![A caixa de diálogo Usuário](./media/active-directory-saas-evidence-tutorial/create_aaduser_04.png)

    <span data-ttu-id="5fc91-190">a.</span><span class="sxs-lookup"><span data-stu-id="5fc91-190">a.</span></span> <span data-ttu-id="5fc91-191">Na caixa **Nome**, digite **BrendaFernandes**.</span><span class="sxs-lookup"><span data-stu-id="5fc91-191">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5fc91-192">b.</span><span class="sxs-lookup"><span data-stu-id="5fc91-192">b.</span></span> <span data-ttu-id="5fc91-193">Na caixa **Nome de usuário**, digite o endereço de email do usuário Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="5fc91-193">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="5fc91-194">c.</span><span class="sxs-lookup"><span data-stu-id="5fc91-194">c.</span></span> <span data-ttu-id="5fc91-195">Marque a caixa de seleção **Mostrar Senha** e, em seguida, anote o valor exibido na caixa **Senha**.</span><span class="sxs-lookup"><span data-stu-id="5fc91-195">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="5fc91-196">d.</span><span class="sxs-lookup"><span data-stu-id="5fc91-196">d.</span></span> <span data-ttu-id="5fc91-197">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="5fc91-197">Click **Create**.</span></span>
 
### <a name="create-a-evidencecom-test-user"></a><span data-ttu-id="5fc91-198">Criar um usuário de teste de Evidence.com</span><span class="sxs-lookup"><span data-stu-id="5fc91-198">Create a Evidence.com test user</span></span>

<span data-ttu-id="5fc91-199">Para que os usuários do AD do Azure possam fazer logon, eles deverão receber a permissão de acesso dentro do aplicativo Evidence.com.</span><span class="sxs-lookup"><span data-stu-id="5fc91-199">For Azure AD users to be able to sign in, they must be provisioned for access inside the Evidence.com application.</span></span> <span data-ttu-id="5fc91-200">Esta seção descreve como criar contas de usuário do AD do Azure no Evidence.com.</span><span class="sxs-lookup"><span data-stu-id="5fc91-200">This section describes how to create Azure AD user accounts inside Evidence.com</span></span>

<span data-ttu-id="5fc91-201">**Para provisionar uma conta de usuário no Evidence.com:**</span><span class="sxs-lookup"><span data-stu-id="5fc91-201">**To provision a user account in Evidence.com:**</span></span>

1. <span data-ttu-id="5fc91-202">Em uma janela do navegador da Web, faça logon no site de sua empresa do Evidence.com como administrador.</span><span class="sxs-lookup"><span data-stu-id="5fc91-202">In a web browser window, log into your Evidence.com company site as an administrator.</span></span>

2. <span data-ttu-id="5fc91-203">Navegue até a guia **Administrador** .</span><span class="sxs-lookup"><span data-stu-id="5fc91-203">Navigate to **Admin** tab.</span></span>

3. <span data-ttu-id="5fc91-204">Clique em **Adicionar Usuário**.</span><span class="sxs-lookup"><span data-stu-id="5fc91-204">Click on **Add User**.</span></span>

4. <span data-ttu-id="5fc91-205">Clique no botão **Adicionar** .</span><span class="sxs-lookup"><span data-stu-id="5fc91-205">Click the **Add** button.</span></span>

5. <span data-ttu-id="5fc91-206">O **Endereço de Email** do usuário adicionado deverá coincidir com o nome de usuário dos usuários no AD do Azure aos quais você deseja conceder acesso.</span><span class="sxs-lookup"><span data-stu-id="5fc91-206">The **Email Address** of the added user must match the username of the users in Azure AD who you wish to give access.</span></span> <span data-ttu-id="5fc91-207">Se o nome de usuário e o endereço de email não tiverem o mesmo valor em sua organização, use a seção **Evidence.com > Atributos > Logon Único** do Portal do Azure para alterar o identificador de nome enviado ao Evidence.com para ser o endereço de email.</span><span class="sxs-lookup"><span data-stu-id="5fc91-207">If the username and email address are not the same value in your organization, you can use the **Evidence.com > Attributes > Single Sign-On** section of the Azure portal to change the nameidenitifer sent to Evidence.com to be the email address.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="5fc91-208">Atribuir o usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="5fc91-208">Assign the Azure AD test user</span></span>

<span data-ttu-id="5fc91-209">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao Evidence.com.</span><span class="sxs-lookup"><span data-stu-id="5fc91-209">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Evidence.com.</span></span>

![Atribuir a função de usuário][200] 

<span data-ttu-id="5fc91-211">**Para atribuir Brenda Fernandes ao Evidence.com, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="5fc91-211">**To assign Britta Simon to Evidence.com, perform the following steps:**</span></span>

1. <span data-ttu-id="5fc91-212">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="5fc91-212">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="5fc91-214">Na lista de aplicativos, selecione **Evidence.com**.</span><span class="sxs-lookup"><span data-stu-id="5fc91-214">In the applications list, select **Evidence.com**.</span></span>

    ![O link do Evidence.com na lista de Aplicativos](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_app.png)  

3. <span data-ttu-id="5fc91-216">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="5fc91-216">In the menu on the left, click **Users and groups**.</span></span>

    ![O link “Usuários e grupos”][202]

4. <span data-ttu-id="5fc91-218">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="5fc91-218">Click **Add** button.</span></span> <span data-ttu-id="5fc91-219">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5fc91-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![O painel Adicionar Atribuição][203]

5. <span data-ttu-id="5fc91-221">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="5fc91-221">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="5fc91-222">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5fc91-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5fc91-223">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5fc91-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="5fc91-224">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="5fc91-224">Test single sign-on</span></span>

<span data-ttu-id="5fc91-225">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="5fc91-225">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="5fc91-226">Ao clicar no bloco Evidence.com no Painel de Acesso, você deverá ser conectado automaticamente ao aplicativo Evidence.com.</span><span class="sxs-lookup"><span data-stu-id="5fc91-226">When you click the Evidence.com tile in the Access Panel, you should get automatically signed-on to your Evidence.com application.</span></span>
<span data-ttu-id="5fc91-227">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5fc91-227">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="5fc91-228">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="5fc91-228">Additional resources</span></span>

* [<span data-ttu-id="5fc91-229">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="5fc91-229">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5fc91-230">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5fc91-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_203.png

