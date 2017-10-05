---
title: "Tutorial: integração do Azure Active Directory com o FilesAnywhere | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o FilesAnywhere."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: jeedes
ms.openlocfilehash: 4153056bd21006061c6ad8ff9cf3c17de9248628
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-filesanywhere"></a><span data-ttu-id="cd79c-103">Tutorial: Integração do Azure Active Directory com o FilesAnywhere</span><span class="sxs-lookup"><span data-stu-id="cd79c-103">Tutorial: Azure Active Directory integration with FilesAnywhere</span></span>

<span data-ttu-id="cd79c-104">Neste tutorial, você aprenderá a integrar o FilesAnywhere ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="cd79c-104">In this tutorial, you learn how to integrate FilesAnywhere with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cd79c-105">A integração do FilesAnywhere com o Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="cd79c-105">Integrating FilesAnywhere with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="cd79c-106">No Azure AD, é possível controlar quem tem acesso ao FilesAnywhere</span><span class="sxs-lookup"><span data-stu-id="cd79c-106">You can control in Azure AD who has access to FilesAnywhere</span></span>
- <span data-ttu-id="cd79c-107">É possível permitir que seus usuários façam logon automaticamente no FilesAnywhere (Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="cd79c-107">You can enable your users to automatically get signed-on to FilesAnywhere (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="cd79c-108">Você pode gerenciar suas contas em um único local - o portal de Gerenciamento do Azure</span><span class="sxs-lookup"><span data-stu-id="cd79c-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="cd79c-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao AD do Azure, consulte [O que é o acesso a aplicativos e logon único com o Active Directory do Azure](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="cd79c-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cd79c-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="cd79c-110">Prerequisites</span></span>

<span data-ttu-id="cd79c-111">Para configurar a integração do Azure AD com o FilesAnywhere, são necessários os seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="cd79c-111">To configure Azure AD integration with FilesAnywhere, you need the following items:</span></span>

- <span data-ttu-id="cd79c-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="cd79c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cd79c-113">Uma assinatura do FilesAnywhere habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="cd79c-113">A FilesAnywhere single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="cd79c-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="cd79c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="cd79c-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="cd79c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cd79c-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="cd79c-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="cd79c-117">Se não tiver um ambiente de avaliação do Azure AD, você poderá obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cd79c-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="cd79c-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="cd79c-118">Scenario description</span></span>
<span data-ttu-id="cd79c-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="cd79c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cd79c-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="cd79c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cd79c-121">Adicionando o FilesAnywhere da galeria</span><span class="sxs-lookup"><span data-stu-id="cd79c-121">Adding FilesAnywhere from the gallery</span></span>
2. <span data-ttu-id="cd79c-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="cd79c-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-filesanywhere-from-the-gallery"></a><span data-ttu-id="cd79c-123">Adicionando o FilesAnywhere da galeria</span><span class="sxs-lookup"><span data-stu-id="cd79c-123">Adding FilesAnywhere from the gallery</span></span>
<span data-ttu-id="cd79c-124">Para configurar a integração do FilesAnywhere com o Azure AD, é necessário adicionar o FilesAnywhere da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="cd79c-124">To configure the integration of FilesAnywhere into Azure AD, you need to add FilesAnywhere from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="cd79c-125">**Para adicionar o FilesAnywhere da galeria, siga as etapas abaixo:**</span><span class="sxs-lookup"><span data-stu-id="cd79c-125">**To add FilesAnywhere from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="cd79c-126">No **[Portal de Gerenciamento do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="cd79c-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="cd79c-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="cd79c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="cd79c-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="cd79c-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="cd79c-131">Clique em **adicionar** botão na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="cd79c-131">Click **Add** button on the top of the dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="cd79c-133">Na caixa de pesquisa, digite **FilesAnywhere**.</span><span class="sxs-lookup"><span data-stu-id="cd79c-133">In the search box, type **FilesAnywhere**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_search.png)

5. <span data-ttu-id="cd79c-135">No painel de resultados, selecione **FilesAnywhere** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="cd79c-135">In the results panel, select **FilesAnywhere**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_addfromgallery.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="cd79c-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="cd79c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="cd79c-138">Nesta seção, você configurará e testará o logon único do Azure AD com o FilesAnywhere, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="cd79c-138">In this section, you configure and test Azure AD single sign-on with FilesAnywhere based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="cd79c-139">Para o logon único funcionar, o Azure AD precisa saber qual usuário do FilesAnywhere é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cd79c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in FilesAnywhere is to a user in Azure AD.</span></span> <span data-ttu-id="cd79c-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado no FilesAnywhere.</span><span class="sxs-lookup"><span data-stu-id="cd79c-140">In other words, a link relationship between an Azure AD user and the related user in FilesAnywhere needs to be established.</span></span>

<span data-ttu-id="cd79c-141">Essa relação de vínculo é estabelecida atribuindo o valor de **nome de usuário** no Azure AD como o valor de **Nome de usuário** no FilesAnywhere.</span><span class="sxs-lookup"><span data-stu-id="cd79c-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in FilesAnywhere.</span></span>

<span data-ttu-id="cd79c-142">Para configurar e testar o logon único do Azure AD com o FilesAnywhere, é necessário concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="cd79c-142">To configure and test Azure AD single sign-on with FilesAnywhere, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="cd79c-143">**[Configuração do logon único do AD do Azure](#configuring-azure-ad-single-sign-on)** : para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="cd79c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="cd79c-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** - para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="cd79c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cd79c-145">**[Criando um usuário de teste do FilesAnywhere](#creating-a-filesanywhere-test-user)** – para ter um equivalente de Brenda Fernandes no FilesAnywhere que esteja vinculado à representação dela no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cd79c-145">**[Creating a FilesAnywhere test user](#creating-a-filesanywhere-test-user)** - to have a counterpart of Britta Simon in FilesAnywhere that is linked to the Azure AD representation of her.</span></span>
3. <span data-ttu-id="cd79c-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="cd79c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
4. <span data-ttu-id="cd79c-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="cd79c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="cd79c-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="cd79c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="cd79c-149">Nesta seção, você habilitará o logon único do Azure AD no Portal de Gerenciamento do Azure e configurará o logon único em seu aplicativo FilesAnywhere.</span><span class="sxs-lookup"><span data-stu-id="cd79c-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your FilesAnywhere application.</span></span>

<span data-ttu-id="cd79c-150">**Para configurar o logon único do Azure AD com o FilesAnywhere, siga as etapas abaixo:**</span><span class="sxs-lookup"><span data-stu-id="cd79c-150">**To configure Azure AD single sign-on with FilesAnywhere, perform the following steps:**</span></span>

1. <span data-ttu-id="cd79c-151">No Portal de Gerenciamento do Azure, na página de integração de aplicativos do **FilesAnywhere**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="cd79c-151">In the Azure Management portal, on the **FilesAnywhere** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="cd79c-153">Na caixa de diálogo **Logon único**, como **Modo**, selecione **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="cd79c-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_samlbase.png)

3. <span data-ttu-id="cd79c-155">Na seção **Domínio e URLs do FilesAnywhere**, se você desejar configurar o aplicativo em **Modo iniciado pelo IdP**:</span><span class="sxs-lookup"><span data-stu-id="cd79c-155">On the **FilesAnywhere Domain and URLs** section, If you wish to configure the application in **IDP initiated mode**:</span></span>

    ![Configurar o logon único](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_filesanywhere_url.png)
    
    <span data-ttu-id="cd79c-157">a.</span><span class="sxs-lookup"><span data-stu-id="cd79c-157">a.</span></span> <span data-ttu-id="cd79c-158">Na caixa de texto **URL de resposta**, digite uma URL no seguinte padrão: `https://<company name>.filesanywhere.com/saml20.aspx?c=215`</span><span class="sxs-lookup"><span data-stu-id="cd79c-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.filesanywhere.com/saml20.aspx?c=215`</span></span>
> [!NOTE]
> <span data-ttu-id="cd79c-159">Observe que o valor **215** é uma **clientid** e é apenas um exemplo.</span><span class="sxs-lookup"><span data-stu-id="cd79c-159">Please note that the value **215** is a **clientid** and is just an example.</span></span> <span data-ttu-id="cd79c-160">É necessário substituí-lo pelo valor de clientid real.</span><span class="sxs-lookup"><span data-stu-id="cd79c-160">You need to replace it with the actual clientid value.</span></span>

4. <span data-ttu-id="cd79c-161">Na seção **Domínio e URLs do FilesAnywhere**, se você desejar configurar o aplicativo no **Modo iniciado por SP**, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="cd79c-161">On the **FilesAnywhere Domain and URLs** section, If you wish to configure the application in **SP initiated mode**, perform the following steps:</span></span>
    
    ![Configurar o logon único](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_filesanywhere_url1.png)

    <span data-ttu-id="cd79c-163">a.</span><span class="sxs-lookup"><span data-stu-id="cd79c-163">a.</span></span> <span data-ttu-id="cd79c-164">Clique na opção **Mostrar URL configurações avançadas**</span><span class="sxs-lookup"><span data-stu-id="cd79c-164">Click on the **Show advanced URL settings** option</span></span>

    <span data-ttu-id="cd79c-165">b.</span><span class="sxs-lookup"><span data-stu-id="cd79c-165">b.</span></span> <span data-ttu-id="cd79c-166">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<sub domain>.filesanywhere.com/`</span><span class="sxs-lookup"><span data-stu-id="cd79c-166">In the **Sign On URL** textbox, type a URL using the following pattern: `https://<sub domain>.filesanywhere.com/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="cd79c-167">Observe que esses não são os valores reais.</span><span class="sxs-lookup"><span data-stu-id="cd79c-167">Please note that these are not the real values.</span></span> <span data-ttu-id="cd79c-168">Você precisa atualizar esses valores com a URL de Entrada e a URL de Resposta reais.</span><span class="sxs-lookup"><span data-stu-id="cd79c-168">You have to update these values with the actual Sign On URL and Reply URL.</span></span> <span data-ttu-id="cd79c-169">Contate a [equipe de suporte do FilesAnywhere](mailto:support@FilesAnywhere.com) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="cd79c-169">Contact [FilesAnywhere support team](mailto:support@FilesAnywhere.com) to get these values.</span></span> 

5. <span data-ttu-id="cd79c-170">O aplicativo FilesAnywhere Software espera que as declarações SAML estejam em um formato específico.</span><span class="sxs-lookup"><span data-stu-id="cd79c-170">FilesAnywhere Software application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="cd79c-171">Configure as seguintes declarações para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="cd79c-171">Please configure the following claims for this application.</span></span> <span data-ttu-id="cd79c-172">Você pode gerenciar os valores desses atributos da seção "**Atributos de Usuário**" na página de integração do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="cd79c-172">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="cd79c-173">A captura de tela a seguir mostra um exemplo disso.</span><span class="sxs-lookup"><span data-stu-id="cd79c-173">The following screenshot shows an example for this.</span></span>
    
    ![Configurar Logon Único](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_filesanywhere_attribute.png)
    
    <span data-ttu-id="cd79c-175">Quando os usuários se inscrevem no FilesAnywhere, eles obtêm o valor do atributo **clientid** da [equipe do FilesAnywhere](mailto:support@FilesAnywhere.com).</span><span class="sxs-lookup"><span data-stu-id="cd79c-175">When the users signs up with FilesAnywhere they get the value of **clientid** attribute from [FilesAnywhere team](mailto:support@FilesAnywhere.com).</span></span> <span data-ttu-id="cd79c-176">É necessário adicionar o atributo "ID do cliente" com o valor exclusivo fornecido pelo FilesAnywhere.</span><span class="sxs-lookup"><span data-stu-id="cd79c-176">You have to add the "Client Id" attribute with the unique value provided by FilesAnywhere.</span></span> <span data-ttu-id="cd79c-177">Todos esses atributos mostrados acima são necessários.</span><span class="sxs-lookup"><span data-stu-id="cd79c-177">All these attributes shown above are required.</span></span>
    > [!NOTE] 
    > <span data-ttu-id="cd79c-178">Observe que o valor **2331** de **clientid** é apenas um exemplo.</span><span class="sxs-lookup"><span data-stu-id="cd79c-178">Please note that the value **2331** of **clientid** is just an example.</span></span> <span data-ttu-id="cd79c-179">É necessário fornecer o valor real.</span><span class="sxs-lookup"><span data-stu-id="cd79c-179">You need to provide the actual value.</span></span>


6. <span data-ttu-id="cd79c-180">Na seção **Atributos do usuário**, na caixa de diálogo **Logon único**, configure o atributo do token SAML na imagem acima e siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="cd79c-180">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>
    
    | <span data-ttu-id="cd79c-181">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="cd79c-181">Attribute Name</span></span> | <span data-ttu-id="cd79c-182">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="cd79c-182">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="cd79c-183">clientid</span><span class="sxs-lookup"><span data-stu-id="cd79c-183">clientid</span></span> | <span data-ttu-id="cd79c-184">*"uniquevalue"*</span><span class="sxs-lookup"><span data-stu-id="cd79c-184">*"uniquevalue"*</span></span> |

    <span data-ttu-id="cd79c-185">a.</span><span class="sxs-lookup"><span data-stu-id="cd79c-185">a.</span></span> <span data-ttu-id="cd79c-186">Clique em **Adicionar atributo** para abrir o diálogo **Adicionar Atributo**.</span><span class="sxs-lookup"><span data-stu-id="cd79c-186">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_04.png)

    ![Configurar Logon Único](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_05.png)
    
    <span data-ttu-id="cd79c-189">b.</span><span class="sxs-lookup"><span data-stu-id="cd79c-189">b.</span></span> <span data-ttu-id="cd79c-190">Na caixa de texto **Nome** , digite o nome do atributo mostrado para essa linha.</span><span class="sxs-lookup"><span data-stu-id="cd79c-190">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="cd79c-191">c.</span><span class="sxs-lookup"><span data-stu-id="cd79c-191">c.</span></span> <span data-ttu-id="cd79c-192">Na lista **Valor**, digite o valor do atributo mostrado para essa linha.</span><span class="sxs-lookup"><span data-stu-id="cd79c-192">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="cd79c-193">d.</span><span class="sxs-lookup"><span data-stu-id="cd79c-193">d.</span></span> <span data-ttu-id="cd79c-194">Clique em **Ok**</span><span class="sxs-lookup"><span data-stu-id="cd79c-194">Click **Ok**</span></span>

7. <span data-ttu-id="cd79c-195">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="cd79c-195">Click **Save** button.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="cd79c-197">Na seção **Certificado de Autenticação SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado em seu computador.</span><span class="sxs-lookup"><span data-stu-id="cd79c-197">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_certificate.png) 

9. <span data-ttu-id="cd79c-199">Na seção **Configuração do FilesAnywhere**, clique em **Configurar o FilesAnywhere** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="cd79c-199">On the **FilesAnywhere Configuration** section, click **Configure FilesAnywhere** to open **Configure sign-on** window.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_configure.png) 

    ![Configurar o logon único](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_configuresignon.png)

10. <span data-ttu-id="cd79c-202">Para obter a configuração de SSO completa para seu aplicativo na extremidade do FilesAnywhere, contate a [equipe de suporte do FilesAnywhere](mailto:support@FilesAnywhere.com) e forneça a eles a URL do certificado e do SSO (Logon único) da assinatura do token SAML.</span><span class="sxs-lookup"><span data-stu-id="cd79c-202">To get SSO configuration complete for your application at FilesAnywhere end, contact [FilesAnywhere support team](mailto:support@FilesAnywhere.com) and provide them the downloaded SAML token signing Certificate and Single Sign On (SSO) URL.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="cd79c-203">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="cd79c-203">Creating an Azure AD test user</span></span>
<span data-ttu-id="cd79c-204">O objetivo desta seção é criar um usuário de teste no Portal de Gerenciamento do Azure chamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cd79c-204">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="cd79c-206">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="cd79c-206">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="cd79c-207">No **portal de Gerenciamento do Azure**, no painel navegação à esquerda, clique em **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="cd79c-207">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="cd79c-209">Vá para **usuários e grupos** e clique em **todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="cd79c-209">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="cd79c-211">Na parte superior da caixa de diálogo clique **adicionar** para abrir o **usuário** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="cd79c-211">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="cd79c-213">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="cd79c-213">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="cd79c-215">a.</span><span class="sxs-lookup"><span data-stu-id="cd79c-215">a.</span></span> <span data-ttu-id="cd79c-216">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="cd79c-216">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cd79c-217">b.</span><span class="sxs-lookup"><span data-stu-id="cd79c-217">b.</span></span> <span data-ttu-id="cd79c-218">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="cd79c-218">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="cd79c-219">c.</span><span class="sxs-lookup"><span data-stu-id="cd79c-219">c.</span></span> <span data-ttu-id="cd79c-220">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="cd79c-220">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="cd79c-221">d.</span><span class="sxs-lookup"><span data-stu-id="cd79c-221">d.</span></span> <span data-ttu-id="cd79c-222">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="cd79c-222">Click **Create**.</span></span> 



### <a name="creating-a-filesanywhere-test-user"></a><span data-ttu-id="cd79c-223">Criando um usuário de teste do FilesAnywhere</span><span class="sxs-lookup"><span data-stu-id="cd79c-223">Creating a FilesAnywhere test user</span></span>

<span data-ttu-id="cd79c-224">O aplicativo dá suporte ao provisionamento de usuário just-in-time e, após a autenticação, os usuários serão automaticamente criados no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="cd79c-224">Application supports Just in time user provisioning and after authentication users will be created in the application automatically.</span></span> 


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="cd79c-225">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="cd79c-225">Assigning the Azure AD test user</span></span>

<span data-ttu-id="cd79c-226">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao FilesAnywhere.</span><span class="sxs-lookup"><span data-stu-id="cd79c-226">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to FilesAnywhere.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="cd79c-228">**Para atribuir Brenda Fernandes ao FilesAnywhere, siga as etapas abaixo:**</span><span class="sxs-lookup"><span data-stu-id="cd79c-228">**To assign Britta Simon to FilesAnywhere, perform the following steps:**</span></span>

1. <span data-ttu-id="cd79c-229">No portal de gerenciamento do Azure, abra a exibição de aplicativos e, em seguida, navegue até o modo de exibição de diretório e vá para **aplicativos empresariais** e clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="cd79c-229">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="cd79c-231">Na lista de aplicativos, escolha **FilesAnywhere**.</span><span class="sxs-lookup"><span data-stu-id="cd79c-231">In the applications list, select **FilesAnywhere**.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_app.png) 

3. <span data-ttu-id="cd79c-233">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="cd79c-233">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="cd79c-235">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="cd79c-235">Click **Add** button.</span></span> <span data-ttu-id="cd79c-236">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="cd79c-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="cd79c-238">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="cd79c-238">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="cd79c-239">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="cd79c-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="cd79c-240">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="cd79c-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="cd79c-241">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="cd79c-241">Testing single sign-on</span></span>

<span data-ttu-id="cd79c-242">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="cd79c-242">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="cd79c-243">Ao clicar no bloco FilesAnywhere no Painel de Acesso, seu logon deverá ser feito automaticamente no aplicativo FilesAnywhere.</span><span class="sxs-lookup"><span data-stu-id="cd79c-243">When you click the FilesAnywhere tile in the Access Panel, you should get automatically signed-on to your FilesAnywhere application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="cd79c-244">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="cd79c-244">Additional resources</span></span>

* [<span data-ttu-id="cd79c-245">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="cd79c-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cd79c-246">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="cd79c-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_203.png
