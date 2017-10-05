---
title: "Tutorial: integração do Azure Active Directory com o Onit | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Onit."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: bc479a28-8fcd-493f-ac53-681975a5149c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: jeedes
ms.openlocfilehash: 47c0055b89dbcf6a30a7f9ac5a33913e7bf463fa
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-onit"></a><span data-ttu-id="50832-103">Tutorial: Integração do Active Directory do Azure com o Onit</span><span class="sxs-lookup"><span data-stu-id="50832-103">Tutorial: Azure Active Directory integration with Onit</span></span>

<span data-ttu-id="50832-104">Neste tutorial, você aprenderá a integrar o Onit ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="50832-104">In this tutorial, you learn how to integrate Onit with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="50832-105">A integração do Onit ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="50832-105">Integrating Onit with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="50832-106">No Azure AD, é possível controlar quem tem acesso ao Onit.</span><span class="sxs-lookup"><span data-stu-id="50832-106">You can control in Azure AD who has access to Onit.</span></span>
- <span data-ttu-id="50832-107">Você pode permitir que os usuários façam logon automaticamente no Onit (logon único) com as respectivas contas do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="50832-107">You can enable your users to automatically get signed-on to Onit (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="50832-108">Você pode gerenciar suas contas em um único local central – o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="50832-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="50832-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="50832-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="50832-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="50832-110">Prerequisites</span></span>

<span data-ttu-id="50832-111">Para configurar a integração do Azure AD ao Onit, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="50832-111">To configure Azure AD integration with Onit, you need the following items:</span></span>

- <span data-ttu-id="50832-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="50832-112">An Azure AD subscription</span></span>
- <span data-ttu-id="50832-113">Uma assinatura habilitada para logon único do Onit</span><span class="sxs-lookup"><span data-stu-id="50832-113">An Onit single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="50832-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="50832-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="50832-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="50832-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="50832-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="50832-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="50832-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="50832-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="50832-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="50832-118">Scenario description</span></span>

<span data-ttu-id="50832-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="50832-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="50832-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="50832-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="50832-121">Adicionar o Onit da galeria</span><span class="sxs-lookup"><span data-stu-id="50832-121">Adding Onit from the gallery</span></span>
2. <span data-ttu-id="50832-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="50832-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-onit-from-the-gallery"></a><span data-ttu-id="50832-123">Adicionar o Onit da galeria</span><span class="sxs-lookup"><span data-stu-id="50832-123">Adding Onit from the gallery</span></span>
<span data-ttu-id="50832-124">Para configurar a integração do Onit ao Azure AD, você precisará adicionar o Onit à sua lista de aplicativos SaaS gerenciados por meio da galeria.</span><span class="sxs-lookup"><span data-stu-id="50832-124">To configure the integration of Onit into Azure AD, you need to add Onit from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="50832-125">**Para adicionar o Onit da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="50832-125">**To add Onit from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="50832-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="50832-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![O botão Azure Active Directory][1]

2. <span data-ttu-id="50832-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="50832-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="50832-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="50832-129">Then go to **All applications**.</span></span>

    ![A folha Aplicativos empresariais][2]
    
3. <span data-ttu-id="50832-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="50832-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![O botão Novo aplicativo][3]

4. <span data-ttu-id="50832-133">Na caixa de pesquisa, digite **Onit**, selecione **Onit** no painel de resultados e, em seguida, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="50832-133">In the search box, type **Onit**, select **Onit** from result panel then click **Add** button to add the application.</span></span>

    ![Onit na lista de resultados](./media/active-directory-saas-onit-tutorial/tutorial_onit_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="50832-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="50832-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="50832-136">Nesta seção, você configurará e testará o logon único do Azure AD com o Onit, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="50832-136">In this section, you configure and test Azure AD single sign-on with Onit based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="50832-137">Para que o logon único funcione, o Azure AD precisa saber qual usuário do Onit é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="50832-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Onit is to a user in Azure AD.</span></span> <span data-ttu-id="50832-138">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado no Onit.</span><span class="sxs-lookup"><span data-stu-id="50832-138">In other words, a link relationship between an Azure AD user and the related user in Onit needs to be established.</span></span>

<span data-ttu-id="50832-139">No Onit, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="50832-139">In Onit, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="50832-140">Para configurar e testar o logon único do Azure AD com o Onit, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="50832-140">To configure and test Azure AD single sign-on with Onit, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="50832-141">**[Configurar o logon único do Azure AD](#configure-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="50832-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="50832-142">**[Criar um usuário de teste do Azure AD](#create-an-azure-ad-test-user)** – para testar o logon único do Azure AD com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="50832-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="50832-143">**[Criar um usuário de teste do Onit](#create-an-onit-test-user)** – para ter um equivalente de Brenda Fernandes no Onit vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="50832-143">**[Create an Onit test user](#create-an-onit-test-user)** - to have a counterpart of Britta Simon in Onit that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="50832-144">**[Atribuir o usuário de teste do Azure AD](#assign-the-azure-ad-test-user)** – para permitir que Brenda Fernandes use o logon único do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="50832-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="50832-145">**[Teste o logon único](#test-single-sign-on)** para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="50832-145">**[Test single sign-on](#test-single-sign-on)** to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="50832-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="50832-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="50832-147">Nesta seção, você habilitará o logon único do Azure AD no Portal do Azure e configurará o logon único no aplicativo Onit.</span><span class="sxs-lookup"><span data-stu-id="50832-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Onit application.</span></span>

<span data-ttu-id="50832-148">**Para configurar o logon único do Azure AD com o Onit, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="50832-148">**To configure Azure AD single sign-on with Onit, perform the following steps:**</span></span>

1. <span data-ttu-id="50832-149">No Portal do Azure, na página de integração de aplicativos do **Onit**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="50832-149">In the Azure portal, on the **Onit** application integration page, click **Single sign-on**.</span></span>

    ![Link Configurar logon único][4]

2. <span data-ttu-id="50832-151">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="50832-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-onit-tutorial/tutorial_onit_samlbase.png)

3. <span data-ttu-id="50832-153">Na seção **Domínio e URLs do Onit**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="50832-153">On the **Onit Domain and URLs** section, perform the following steps:</span></span>

    ![Informações de logon único de Domínio e URLs do Onit](./media/active-directory-saas-onit-tutorial/tutorial_onit_url.png)

    <span data-ttu-id="50832-155">a.</span><span class="sxs-lookup"><span data-stu-id="50832-155">a.</span></span> <span data-ttu-id="50832-156">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<sub-domain>.onit.com`</span><span class="sxs-lookup"><span data-stu-id="50832-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<sub-domain>.onit.com`</span></span>

    <span data-ttu-id="50832-157">b.</span><span class="sxs-lookup"><span data-stu-id="50832-157">b.</span></span> <span data-ttu-id="50832-158">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<sub-domain>.onit.com`</span><span class="sxs-lookup"><span data-stu-id="50832-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<sub-domain>.onit.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="50832-159">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="50832-159">These values are not real.</span></span> <span data-ttu-id="50832-160">Atualize esses valores com a URL de Entrada e o Identificador reais.</span><span class="sxs-lookup"><span data-stu-id="50832-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="50832-161">Contate a [equipe de suporte ao cliente do Onit](https://www.onit.com/support) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="50832-161">Contact [Onit Client support team](https://www.onit.com/support) to get these values.</span></span> 
 
4. <span data-ttu-id="50832-162">Na seção **Certificado de Autenticação SAML**, copie o valor da **IMPRESSÃO DIGITAL** do certificado.</span><span class="sxs-lookup"><span data-stu-id="50832-162">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value of certificate.</span></span>

    ![O link de download do Certificado](./media/active-directory-saas-onit-tutorial/tutorial_onit_certificate.png) 

5. <span data-ttu-id="50832-164">O aplicativo Onit espera que as declarações SAML estejam em um formato específico.</span><span class="sxs-lookup"><span data-stu-id="50832-164">Onit application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="50832-165">Configure as seguintes declarações para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="50832-165">Please configure the following claims for this application.</span></span> <span data-ttu-id="50832-166">Você pode gerenciar o valor dos atributos na guia **"Atributo"** do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="50832-166">You can manage the values of these attributes from the **"Atrribute"** tab of the application.</span></span> <span data-ttu-id="50832-167">A captura de tela a seguir mostra um exemplo disso.</span><span class="sxs-lookup"><span data-stu-id="50832-167">The following screenshot shows an example for this.</span></span> 

    ![Configurar Logon Único](./media/active-directory-saas-onit-tutorial/tutorial_onit_attribute.png) 

6. <span data-ttu-id="50832-169">Na seção **Atributos do Usuário**, na caixa de diálogo **Logon único**, configure o atributo do token SAML como mostra a imagem e execute as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="50832-169">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="50832-170">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="50832-170">Attribute Name</span></span> | <span data-ttu-id="50832-171">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="50832-171">Attribute Value</span></span> |
    | ------------------- | -------------------- |
    | <span data-ttu-id="50832-172">email</span><span class="sxs-lookup"><span data-stu-id="50832-172">email</span></span> | <span data-ttu-id="50832-173">user.mail</span><span class="sxs-lookup"><span data-stu-id="50832-173">user.mail</span></span> |
    
    <span data-ttu-id="50832-174">a.</span><span class="sxs-lookup"><span data-stu-id="50832-174">a.</span></span> <span data-ttu-id="50832-175">Clique em **Adicionar atributo** para abrir o diálogo **Adicionar Atributo**.</span><span class="sxs-lookup"><span data-stu-id="50832-175">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-onit-tutorial/tutorial_attribute_04.png)

    ![Configurar Logon Único](./media/active-directory-saas-onit-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="50832-178">b.</span><span class="sxs-lookup"><span data-stu-id="50832-178">b.</span></span> <span data-ttu-id="50832-179">Na caixa de texto **Nome** , digite o nome do atributo mostrado para essa linha.</span><span class="sxs-lookup"><span data-stu-id="50832-179">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="50832-180">c.</span><span class="sxs-lookup"><span data-stu-id="50832-180">c.</span></span> <span data-ttu-id="50832-181">Na lista **Valor**, digite o valor do atributo mostrado para essa linha.</span><span class="sxs-lookup"><span data-stu-id="50832-181">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="50832-182">d.</span><span class="sxs-lookup"><span data-stu-id="50832-182">d.</span></span> <span data-ttu-id="50832-183">Deixe o **Namespace** em branco.</span><span class="sxs-lookup"><span data-stu-id="50832-183">Leave the **Namespace** blank.</span></span>
    
    <span data-ttu-id="50832-184">e.</span><span class="sxs-lookup"><span data-stu-id="50832-184">e.</span></span> <span data-ttu-id="50832-185">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="50832-185">Click **Ok**.</span></span>

7. <span data-ttu-id="50832-186">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="50832-186">Click **Save** button.</span></span>

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-onit-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="50832-188">Na seção **Configuração do Onit**, clique em **Configurar o Onit** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="50832-188">On the **Onit Configuration** section, click **Configure Onit** to open **Configure sign-on** window.</span></span> <span data-ttu-id="50832-189">Copie a **URL do Serviço de Logon Único do SAML e a URL de logoff** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="50832-189">Copy the **Sign-Out URL, SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configuração do Onit](./media/active-directory-saas-onit-tutorial/tutorial_onit_configure.png)

9. <span data-ttu-id="50832-191">Em outra janela do navegador da Web, faça logon em seu site de empresa Onit como um administrador.</span><span class="sxs-lookup"><span data-stu-id="50832-191">In a different web browser window, log into your Onit company site as an administrator.</span></span>

10. <span data-ttu-id="50832-192">No menu na parte superior, clique em **Administração**.</span><span class="sxs-lookup"><span data-stu-id="50832-192">In the menu on the top, click **Administration**.</span></span>
   
   <span data-ttu-id="50832-193">![Administração](./media/active-directory-saas-onit-tutorial/IC791174.png "Administração")</span><span class="sxs-lookup"><span data-stu-id="50832-193">![Administration](./media/active-directory-saas-onit-tutorial/IC791174.png "Administration")</span></span>
11. <span data-ttu-id="50832-194">Clique em **Editar Empresa**.</span><span class="sxs-lookup"><span data-stu-id="50832-194">Click **Edit Corporation**.</span></span>
   
   <span data-ttu-id="50832-195">![Editar Corporação](./media/active-directory-saas-onit-tutorial/IC791175.png "Editar Corporação")</span><span class="sxs-lookup"><span data-stu-id="50832-195">![Edit Corporation](./media/active-directory-saas-onit-tutorial/IC791175.png "Edit Corporation")</span></span>
   
12. <span data-ttu-id="50832-196">Clique na guia **Segurança** .</span><span class="sxs-lookup"><span data-stu-id="50832-196">Click the **Security** tab.</span></span>
    
    <span data-ttu-id="50832-197">![Editar Informações da Empresa](./media/active-directory-saas-onit-tutorial/IC791176.png "Editar Informações da Empresa")</span><span class="sxs-lookup"><span data-stu-id="50832-197">![Edit Company Information](./media/active-directory-saas-onit-tutorial/IC791176.png "Edit Company Information")</span></span>

13. <span data-ttu-id="50832-198">Na guia **Segurança** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="50832-198">On the **Security** tab, perform the following steps:</span></span>

    <span data-ttu-id="50832-199">![Logon Único](./media/active-directory-saas-onit-tutorial/IC791177.png "Logon Único")</span><span class="sxs-lookup"><span data-stu-id="50832-199">![Single Sign-On](./media/active-directory-saas-onit-tutorial/IC791177.png "Single Sign-On")</span></span>

    <span data-ttu-id="50832-200">a.</span><span class="sxs-lookup"><span data-stu-id="50832-200">a.</span></span> <span data-ttu-id="50832-201">Como **Estratégia de Autenticação**, selecione **Logn Único e Senha**.</span><span class="sxs-lookup"><span data-stu-id="50832-201">As **Authentication Strategy**, select **Single Sign On and Password**.</span></span>
    
    <span data-ttu-id="50832-202">b.</span><span class="sxs-lookup"><span data-stu-id="50832-202">b.</span></span> <span data-ttu-id="50832-203">Na caixa de texto **URL de Destino do IdP**, cole o valor da **URL do Serviço de Logon Único SAML** copiado do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="50832-203">In **Idp Target URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="50832-204">c.</span><span class="sxs-lookup"><span data-stu-id="50832-204">c.</span></span> <span data-ttu-id="50832-205">Na caixa de texto **URL de Logoff do IDP**, cole o valor da **URL de Saída** copiado do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="50832-205">In **Idp logout URL** textbox, paste the value of  **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="50832-206">d.</span><span class="sxs-lookup"><span data-stu-id="50832-206">d.</span></span> <span data-ttu-id="50832-207">Na caixa de texto **Impressão Digital do Certificado IdP (SHA1)**, cole o valor da **Impressão Digital** do certificado copiado do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="50832-207">In **Idp Cert Fingerprint (SHA1)** textbox, paste the  **Thumbprint** value of certificate, which you have copied from Azure portal.</span></span>

> [!TIP]
> <span data-ttu-id="50832-208">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="50832-208">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="50832-209">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="50832-209">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="50832-210">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="50832-210">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="50832-211">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="50832-211">Create an Azure AD test user</span></span>

<span data-ttu-id="50832-212">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="50832-212">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Criar um usuário de teste do Azure AD][100]

<span data-ttu-id="50832-214">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="50832-214">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="50832-215">No portal do Azure, no painel esquerdo, clique no botão **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="50832-215">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![O botão Azure Active Directory](./media/active-directory-saas-onit-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="50832-217">Para exibir a lista de usuários, acesse **Usuários e grupos** e, depois, clique em **Todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="50832-217">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Os links “Usuários e grupos” e “Todos os usuários”](./media/active-directory-saas-onit-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="50832-219">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo **Todos os Usuários**.</span><span class="sxs-lookup"><span data-stu-id="50832-219">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![O botão Adicionar](./media/active-directory-saas-onit-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="50832-221">Na caixa de diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="50832-221">In the **User** dialog box, perform the following steps:</span></span>

    ![A caixa de diálogo Usuário](./media/active-directory-saas-onit-tutorial/create_aaduser_04.png)

    <span data-ttu-id="50832-223">a.</span><span class="sxs-lookup"><span data-stu-id="50832-223">a.</span></span> <span data-ttu-id="50832-224">Na caixa **Nome**, digite **BrendaFernandes**.</span><span class="sxs-lookup"><span data-stu-id="50832-224">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="50832-225">b.</span><span class="sxs-lookup"><span data-stu-id="50832-225">b.</span></span> <span data-ttu-id="50832-226">Na caixa **Nome de usuário**, digite o endereço de email do usuário Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="50832-226">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="50832-227">c.</span><span class="sxs-lookup"><span data-stu-id="50832-227">c.</span></span> <span data-ttu-id="50832-228">Marque a caixa de seleção **Mostrar Senha** e, em seguida, anote o valor exibido na caixa **Senha**.</span><span class="sxs-lookup"><span data-stu-id="50832-228">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="50832-229">d.</span><span class="sxs-lookup"><span data-stu-id="50832-229">d.</span></span> <span data-ttu-id="50832-230">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="50832-230">Click **Create**.</span></span>
 
### <a name="create-an-onit-test-user"></a><span data-ttu-id="50832-231">Criar um usuário de teste do Onit</span><span class="sxs-lookup"><span data-stu-id="50832-231">Create an Onit test user</span></span>

<span data-ttu-id="50832-232">Para permitir que os usuários do AD do Azure façam logon no Onit, eles devem ser provisionados no Onit.</span><span class="sxs-lookup"><span data-stu-id="50832-232">In order to enable Azure AD users to log into Onit, they must be provisioned into Onit.</span></span>  

<span data-ttu-id="50832-233">No caso do Onit, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="50832-233">In the case of Onit, provisioning is a manual task.</span></span>

<span data-ttu-id="50832-234">**Para configurar o provisionamento de usuários, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="50832-234">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="50832-235">Faça logon em seu site de empresa do **Onit** como administrador.</span><span class="sxs-lookup"><span data-stu-id="50832-235">Sign on to your **Onit** company site as an administrator.</span></span>
2. <span data-ttu-id="50832-236">Clique em **Adicionar Usuário**.</span><span class="sxs-lookup"><span data-stu-id="50832-236">Click **Add User**.</span></span>
   
   <span data-ttu-id="50832-237">![Administração](./media/active-directory-saas-onit-tutorial/IC791180.png "Administração")</span><span class="sxs-lookup"><span data-stu-id="50832-237">![Administration](./media/active-directory-saas-onit-tutorial/IC791180.png "Administration")</span></span>
3. <span data-ttu-id="50832-238">Na página do diálogo **Adicionar usuário** , realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="50832-238">On the **Add User** dialog page, perform the following steps:</span></span>
   
   <span data-ttu-id="50832-239">![Adicionar Usuário](./media/active-directory-saas-onit-tutorial/IC791181.png "Adicionar Usuário")</span><span class="sxs-lookup"><span data-stu-id="50832-239">![Add User](./media/active-directory-saas-onit-tutorial/IC791181.png "Add User")</span></span>
   
  1. <span data-ttu-id="50832-240">Digite o **Nome** e **Endereço de Email** de uma conta válida do Azure AD que você deseja provisionar nas caixas de texto relacionadas.</span><span class="sxs-lookup"><span data-stu-id="50832-240">Type the **Name** and the **Email Address** of a valid Azure AD account you want to provision into the related textboxes.</span></span>
  2. <span data-ttu-id="50832-241">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="50832-241">Click **Create**.</span></span>    
   
 > [!NOTE]
 > <span data-ttu-id="50832-242">O titular da conta do Azure Active Directory recebe um email e segue um link para confirmar sua conta antes que ela se torne ativa.</span><span class="sxs-lookup"><span data-stu-id="50832-242">The Azure Active Directory account holder receives an email and follows a link to confirm their account before it becomes active.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="50832-243">Atribuir o usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="50832-243">Assign the Azure AD test user</span></span>

<span data-ttu-id="50832-244">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao Onit.</span><span class="sxs-lookup"><span data-stu-id="50832-244">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Onit.</span></span>

![Atribuir a função de usuário][200] 

<span data-ttu-id="50832-246">**Para atribuir Brenda Fernandes ao Onit, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="50832-246">**To assign Britta Simon to Onit, perform the following steps:**</span></span>

1. <span data-ttu-id="50832-247">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="50832-247">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="50832-249">Na lista de aplicativos, selecione **Onit**.</span><span class="sxs-lookup"><span data-stu-id="50832-249">In the applications list, select **Onit**.</span></span>

    ![O link do Onit na lista de Aplicativos](./media/active-directory-saas-onit-tutorial/tutorial_onit_app.png)  

3. <span data-ttu-id="50832-251">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="50832-251">In the menu on the left, click **Users and groups**.</span></span>

    ![O link “Usuários e grupos”][202]

4. <span data-ttu-id="50832-253">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="50832-253">Click **Add** button.</span></span> <span data-ttu-id="50832-254">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="50832-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![O painel Adicionar Atribuição][203]

5. <span data-ttu-id="50832-256">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="50832-256">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="50832-257">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="50832-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="50832-258">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="50832-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="50832-259">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="50832-259">Test single sign-on</span></span>

<span data-ttu-id="50832-260">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="50832-260">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="50832-261">Ao clicar no bloco do Onit no Painel de Acesso, você deverá ser conectado automaticamente ao aplicativo Onit.</span><span class="sxs-lookup"><span data-stu-id="50832-261">When you click the Onit tile in the Access Panel, you should get automatically signed-on to your Onit application.</span></span>
<span data-ttu-id="50832-262">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="50832-262">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="50832-263">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="50832-263">Additional resources</span></span>

* [<span data-ttu-id="50832-264">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="50832-264">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="50832-265">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="50832-265">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-onit-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-onit-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-onit-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-onit-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-onit-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-onit-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-onit-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-onit-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-onit-tutorial/tutorial_general_203.png

