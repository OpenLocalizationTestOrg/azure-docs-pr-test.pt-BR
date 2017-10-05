---
title: "Tutorial: integração do Azure Active Directory com o M-Files | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o M-Files."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4536fd49-3a65-4cff-9620-860904f726d0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 0f2682cf7cd3e11a5a7156938fbe9d4c7f541312
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-m-files"></a><span data-ttu-id="3b26f-103">Tutorial: integração do Azure Active Directory com o M-Files</span><span class="sxs-lookup"><span data-stu-id="3b26f-103">Tutorial: Azure Active Directory integration with M-Files</span></span>

<span data-ttu-id="3b26f-104">Neste tutorial, você aprenderá a integrar o M-Files ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="3b26f-104">In this tutorial, you learn how to integrate M-Files with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3b26f-105">A integração do M-Files ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="3b26f-105">Integrating M-Files with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3b26f-106">No Azure AD, você pode controlar quem tem acesso ao M-Files</span><span class="sxs-lookup"><span data-stu-id="3b26f-106">You can control in Azure AD who has access to M-Files</span></span>
- <span data-ttu-id="3b26f-107">Você pode permitir que os usuários entrem automaticamente no M-Files (Logon único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="3b26f-107">You can enable your users to automatically get signed-on to M-Files (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3b26f-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="3b26f-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="3b26f-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3b26f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3b26f-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="3b26f-110">Prerequisites</span></span>

<span data-ttu-id="3b26f-111">Para configurar a integração do Azure AD com o M-Files, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="3b26f-111">To configure Azure AD integration with M-Files, you need the following items:</span></span>

- <span data-ttu-id="3b26f-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3b26f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3b26f-113">Uma assinatura habilitada para logon único do M-Files</span><span class="sxs-lookup"><span data-stu-id="3b26f-113">A M-Files single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3b26f-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="3b26f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3b26f-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="3b26f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3b26f-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="3b26f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3b26f-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3b26f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3b26f-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="3b26f-118">Scenario description</span></span>
<span data-ttu-id="3b26f-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="3b26f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3b26f-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="3b26f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3b26f-121">Adicionando o M-Files da galeria</span><span class="sxs-lookup"><span data-stu-id="3b26f-121">Adding M-Files from the gallery</span></span>
2. <span data-ttu-id="3b26f-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3b26f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-m-files-from-the-gallery"></a><span data-ttu-id="3b26f-123">Adicionando o M-Files da galeria</span><span class="sxs-lookup"><span data-stu-id="3b26f-123">Adding M-Files from the gallery</span></span>
<span data-ttu-id="3b26f-124">Para configurar a integração do M-Files ao Azure AD, você precisará adicionar o M-Files da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="3b26f-124">To configure the integration of M-Files into Azure AD, you need to add M-Files from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3b26f-125">**Para adicionar o M-Files da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="3b26f-125">**To add M-Files from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3b26f-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3b26f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3b26f-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="3b26f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="3b26f-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="3b26f-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="3b26f-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3b26f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="3b26f-133">Na caixa de pesquisa, digite **M-Files**.</span><span class="sxs-lookup"><span data-stu-id="3b26f-133">In the search box, type **M-Files**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_search.png)

5. <span data-ttu-id="3b26f-135">No painel de resultados, selecione **M-Files** e, em seguida, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3b26f-135">In the results panel, select **M-Files**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3b26f-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3b26f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3b26f-138">Nesta seção, você configurará e testará o logon único do Azure AD com o M-Files, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="3b26f-138">In this section, you configure and test Azure AD single sign-on with M-Files based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3b26f-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do M-Files é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3b26f-139">For single sign-on to work, Azure AD needs to know what the counterpart user in M-Files is to a user in Azure AD.</span></span> <span data-ttu-id="3b26f-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do M-Files.</span><span class="sxs-lookup"><span data-stu-id="3b26f-140">In other words, a link relationship between an Azure AD user and the related user in M-Files needs to be established.</span></span>

<span data-ttu-id="3b26f-141">No M-Files, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="3b26f-141">In M-Files, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="3b26f-142">Para configurar e testar o logon único do Azure AD com o M-Files, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="3b26f-142">To configure and test Azure AD single sign-on with M-Files, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3b26f-143">**[Configuração do logon único do AD do Azure](#configuring-azure-ad-single-sign-on)** - para permitir que seus usuários usem esse recurso.</span><span class="sxs-lookup"><span data-stu-id="3b26f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3b26f-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="3b26f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3b26f-145">**[Criando um usuário de teste do M-Files](#creating-a-m-files-test-user)**: para ter um equivalente de Brenda Fernandes no M-Files que esteja vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3b26f-145">**[Creating a M-Files test user](#creating-a-m-files-test-user)** - to have a counterpart of Britta Simon in M-Files that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="3b26f-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="3b26f-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3b26f-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="3b26f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3b26f-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="3b26f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3b26f-149">Nesta seção, você habilitará o logon único do Azure AD no Portal do Azure e configurará o logon único em seu aplicativo M-Files.</span><span class="sxs-lookup"><span data-stu-id="3b26f-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your M-Files application.</span></span>

<span data-ttu-id="3b26f-150">**Para configurar o logon único do Azure AD com o M-Files, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="3b26f-150">**To configure Azure AD single sign-on with M-Files, perform the following steps:**</span></span>

1. <span data-ttu-id="3b26f-151">No portal do Azure, na página de integração de aplicativos do **M-Files**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="3b26f-151">In the Azure portal, on the **M-Files** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="3b26f-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="3b26f-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_samlbase.png)

3. <span data-ttu-id="3b26f-155">Na seção **URLs e Domínio do M-Files**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="3b26f-155">On the **M-Files Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_url.png)

    <span data-ttu-id="3b26f-157">a.</span><span class="sxs-lookup"><span data-stu-id="3b26f-157">a.</span></span> <span data-ttu-id="3b26f-158">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<tenantname>.cloudvault.m-files.com/authentication/MFiles.AuthenticationProviders.Core/sso`</span><span class="sxs-lookup"><span data-stu-id="3b26f-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenantname>.cloudvault.m-files.com/authentication/MFiles.AuthenticationProviders.Core/sso`</span></span>

    <span data-ttu-id="3b26f-159">b.</span><span class="sxs-lookup"><span data-stu-id="3b26f-159">b.</span></span> <span data-ttu-id="3b26f-160">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<tenantname>.cloudvault.m-files.com`</span><span class="sxs-lookup"><span data-stu-id="3b26f-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<tenantname>.cloudvault.m-files.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3b26f-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="3b26f-161">These values are not real.</span></span> <span data-ttu-id="3b26f-162">Atualize esses valores com a URL de Entrada e o Identificador reais.</span><span class="sxs-lookup"><span data-stu-id="3b26f-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="3b26f-163">Contate a [equipe de suporte do Cliente M-Files](mailto:support@m-files.com) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="3b26f-163">Contact [M-Files Client support team](mailto:support@m-files.com) to get these values.</span></span> 
 
4. <span data-ttu-id="3b26f-164">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="3b26f-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_certificate.png) 

5. <span data-ttu-id="3b26f-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="3b26f-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-m-files-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="3b26f-168">Para que o SSO seja configurado para o aplicativo, entre em contato com a [equipe de suporte do M-Files](mailto:support@m-files.com) e forneça os metadados baixados.</span><span class="sxs-lookup"><span data-stu-id="3b26f-168">To get SSO configured for your application, contact [M-Files support team](mailto:support@m-files.com) and provide them the downloaded Metadata.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="3b26f-169">Siga as próximas etapas se quiser configurar o SSO para o aplicativo da área de trabalho do M-Files.</span><span class="sxs-lookup"><span data-stu-id="3b26f-169">Follow the next steps if you want to configure SSO for you M-File desktop application.</span></span> <span data-ttu-id="3b26f-170">Nenhuma etapa adicional é necessária se você quer apenas configurar o SSO para versão Web do M-Files.</span><span class="sxs-lookup"><span data-stu-id="3b26f-170">No extra steps are required if you only want to configure SSO for M-Files web version.</span></span>  

7. <span data-ttu-id="3b26f-171">Siga as próximas etapas para configurar o aplicativo da área de trabalho do M-Files a fim de habilitar o SSO com o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3b26f-171">Follow the next steps to configure the M-File desktop application to enable SSO with Azure AD.</span></span> <span data-ttu-id="3b26f-172">Para baixar o M-Files, vá para a página [Baixar M-Files](https://www.m-files.com/en/download-latest-version).</span><span class="sxs-lookup"><span data-stu-id="3b26f-172">To download M-Files, go to [M-Files download](https://www.m-files.com/en/download-latest-version) page.</span></span>

8. <span data-ttu-id="3b26f-173">Abra a janela **Configurações da área de trabalho do M-Files**.</span><span class="sxs-lookup"><span data-stu-id="3b26f-173">Open the **M-Files Desktop Settings** window.</span></span> <span data-ttu-id="3b26f-174">Em seguida, clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="3b26f-174">Then, click **Add**.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-m-files-tutorial/tutorial_m_files_10.png)

9. <span data-ttu-id="3b26f-176">Na janela **Propriedades de Conexão do Cofre de Documentos**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="3b26f-176">On the **Document Vault Connection Properties** window, perform the following steps:</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-m-files-tutorial/tutorial_m_files_11.png)  

    <span data-ttu-id="3b26f-178">No tipo de seção Servidor, os valores são os seguintes:</span><span class="sxs-lookup"><span data-stu-id="3b26f-178">Under the Server section type, the values as follows:</span></span>  

    <span data-ttu-id="3b26f-179">a.</span><span class="sxs-lookup"><span data-stu-id="3b26f-179">a.</span></span> <span data-ttu-id="3b26f-180">Para **Nome**, digite `<tenant-name>.cloudvault.m-files.com`.</span><span class="sxs-lookup"><span data-stu-id="3b26f-180">For **Name**, type `<tenant-name>.cloudvault.m-files.com`.</span></span> 
 
    <span data-ttu-id="3b26f-181">b.</span><span class="sxs-lookup"><span data-stu-id="3b26f-181">b.</span></span> <span data-ttu-id="3b26f-182">Para **Número de Porta**, digite **4466**.</span><span class="sxs-lookup"><span data-stu-id="3b26f-182">For **Port Number**, type **4466**.</span></span> 

    <span data-ttu-id="3b26f-183">c.</span><span class="sxs-lookup"><span data-stu-id="3b26f-183">c.</span></span> <span data-ttu-id="3b26f-184">Para **Protocolo**, selecione **HTTPS**.</span><span class="sxs-lookup"><span data-stu-id="3b26f-184">For **Protocol**, select **HTTPS**.</span></span> 

    <span data-ttu-id="3b26f-185">d.</span><span class="sxs-lookup"><span data-stu-id="3b26f-185">d.</span></span> <span data-ttu-id="3b26f-186">No campo **Autenticação**, selecione **Usuário específico do Windows**.</span><span class="sxs-lookup"><span data-stu-id="3b26f-186">In the **Authentication** field, select **Specific Windows user**.</span></span> <span data-ttu-id="3b26f-187">Em seguida, você verá uma página de entrada.</span><span class="sxs-lookup"><span data-stu-id="3b26f-187">Then, you are prompted with a signing page.</span></span> <span data-ttu-id="3b26f-188">Insira suas credenciais do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3b26f-188">Insert your Azure AD credentials.</span></span> 

    <span data-ttu-id="3b26f-189">e.</span><span class="sxs-lookup"><span data-stu-id="3b26f-189">e.</span></span> <span data-ttu-id="3b26f-190">Para o **Cofre no Servidor**, selecione o cofre correspondente no servidor.</span><span class="sxs-lookup"><span data-stu-id="3b26f-190">For the **Vault on Server**,  select the corresponding vault on server.</span></span>
 
    <span data-ttu-id="3b26f-191">f.</span><span class="sxs-lookup"><span data-stu-id="3b26f-191">f.</span></span> <span data-ttu-id="3b26f-192">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="3b26f-192">Click **OK**.</span></span>

> [!TIP]
> <span data-ttu-id="3b26f-193">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="3b26f-193">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="3b26f-194">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="3b26f-194">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="3b26f-195">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3b26f-195">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3b26f-196">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3b26f-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="3b26f-197">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="3b26f-197">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="3b26f-199">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="3b26f-199">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3b26f-200">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3b26f-200">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-m-files-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3b26f-202">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="3b26f-202">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-m-files-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3b26f-204">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3b26f-204">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-m-files-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3b26f-206">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="3b26f-206">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-m-files-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3b26f-208">a.</span><span class="sxs-lookup"><span data-stu-id="3b26f-208">a.</span></span> <span data-ttu-id="3b26f-209">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="3b26f-209">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3b26f-210">b.</span><span class="sxs-lookup"><span data-stu-id="3b26f-210">b.</span></span> <span data-ttu-id="3b26f-211">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="3b26f-211">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3b26f-212">c.</span><span class="sxs-lookup"><span data-stu-id="3b26f-212">c.</span></span> <span data-ttu-id="3b26f-213">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="3b26f-213">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="3b26f-214">d.</span><span class="sxs-lookup"><span data-stu-id="3b26f-214">d.</span></span> <span data-ttu-id="3b26f-215">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="3b26f-215">Click **Create**.</span></span>
 
### <a name="creating-a-m-files-test-user"></a><span data-ttu-id="3b26f-216">Criar um usuário de teste do M-Files</span><span class="sxs-lookup"><span data-stu-id="3b26f-216">Creating a M-Files test user</span></span>

<span data-ttu-id="3b26f-217">O objetivo desta seção é criar um usuário chamado Brenda Fernandes no M-Files.</span><span class="sxs-lookup"><span data-stu-id="3b26f-217">The objective of this section is to create a user called Britta Simon in M-Files.</span></span> <span data-ttu-id="3b26f-218">Trabalhe com a [equipe de suporte do M-Files](mailto:support@m-files.com) para adicionar os usuários no M-Files.</span><span class="sxs-lookup"><span data-stu-id="3b26f-218">Work with  [M-Files support team](mailto:support@m-files.com) to add the users in the M-Files.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="3b26f-219">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3b26f-219">Assigning the Azure AD test user</span></span>

<span data-ttu-id="3b26f-220">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure ao conceder acesso ao M-Files.</span><span class="sxs-lookup"><span data-stu-id="3b26f-220">In this section, you enable Britta Simon to use Azure single sign-on by granting access to M-Files.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="3b26f-222">**Para atribuir Brenda Fernandes ao M-Files, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="3b26f-222">**To assign Britta Simon to M-Files, perform the following steps:**</span></span>

1. <span data-ttu-id="3b26f-223">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="3b26f-223">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="3b26f-225">Na lista de aplicativos, selecione **M-Files**.</span><span class="sxs-lookup"><span data-stu-id="3b26f-225">In the applications list, select **M-Files**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_app.png) 

3. <span data-ttu-id="3b26f-227">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="3b26f-227">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="3b26f-229">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="3b26f-229">Click **Add** button.</span></span> <span data-ttu-id="3b26f-230">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3b26f-230">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="3b26f-232">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="3b26f-232">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="3b26f-233">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3b26f-233">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3b26f-234">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3b26f-234">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3b26f-235">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="3b26f-235">Testing single sign-on</span></span>

<span data-ttu-id="3b26f-236">O objetivo desta seção é testar sua configuração de SSO do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="3b26f-236">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="3b26f-237">Ao clicar no bloco M-Files no Painel de Acesso, você deverá ser conectado automaticamente ao aplicativo M-Files.</span><span class="sxs-lookup"><span data-stu-id="3b26f-237">When you click the M-Files tile in the Access Panel, you should get automatically signed-on to your M-Files application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3b26f-238">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="3b26f-238">Additional resources</span></span>

* [<span data-ttu-id="3b26f-239">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="3b26f-239">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3b26f-240">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3b26f-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_203.png

