---
title: "Tutorial: Integração do Azure Active Directory com o SD Elements | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Active Directory do Azure e o SD Elements."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f0386307-bb3b-4810-8d4b-d0bfebda04f4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 624eff0a0da8f548877e4a4346b21df89cd37b67
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sd-elements"></a><span data-ttu-id="4420f-103">Tutorial: Integração do Active Directory do Azure com SD Elements</span><span class="sxs-lookup"><span data-stu-id="4420f-103">Tutorial: Azure Active Directory integration with SD Elements</span></span>

<span data-ttu-id="4420f-104">Neste tutorial, você aprende a integrar o SD Elements ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="4420f-104">In this tutorial, you learn how to integrate SD Elements with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4420f-105">A integração do SD Elements ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="4420f-105">Integrating SD Elements with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="4420f-106">No AD do Azure, você pode controlar quem tem acesso ao SD Elements</span><span class="sxs-lookup"><span data-stu-id="4420f-106">You can control in Azure AD who has access to SD Elements</span></span>
- <span data-ttu-id="4420f-107">Você pode habilitar seus usuários a fazerem logon automaticamente em SD Elements (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4420f-107">You can enable your users to automatically get signed-on to SD Elements (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4420f-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="4420f-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="4420f-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4420f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4420f-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="4420f-110">Prerequisites</span></span>

<span data-ttu-id="4420f-111">Para configurar a integração do AD do Azure a SD Elements, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="4420f-111">To configure Azure AD integration with SD Elements, you need the following items:</span></span>

- <span data-ttu-id="4420f-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4420f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4420f-113">Uma assinatura habilitada para logon único do SD Elements</span><span class="sxs-lookup"><span data-stu-id="4420f-113">A SD Elements single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4420f-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="4420f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4420f-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="4420f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4420f-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="4420f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4420f-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4420f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4420f-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="4420f-118">Scenario description</span></span>
<span data-ttu-id="4420f-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="4420f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4420f-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="4420f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4420f-121">Adicionando elementos SD da galeria</span><span class="sxs-lookup"><span data-stu-id="4420f-121">Adding SD Elements from the gallery</span></span>
2. <span data-ttu-id="4420f-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4420f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sd-elements-from-the-gallery"></a><span data-ttu-id="4420f-123">Adicionando elementos SD da galeria</span><span class="sxs-lookup"><span data-stu-id="4420f-123">Adding SD Elements from the gallery</span></span>
<span data-ttu-id="4420f-124">Para configurar a integração de SD Elements ao Azure AD, você precisa adicionar SD Elements da galeria à sua lista de aplicativos de SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="4420f-124">To configure the integration of SD Elements into Azure AD, you need to add SD Elements from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="4420f-125">**Para adicionar SD Elements da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="4420f-125">**To add SD Elements from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="4420f-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4420f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4420f-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="4420f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="4420f-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="4420f-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="4420f-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4420f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="4420f-133">Na caixa de pesquisa, digite **SD Elements**.</span><span class="sxs-lookup"><span data-stu-id="4420f-133">In the search box, type **SD Elements**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_search.png)

5. <span data-ttu-id="4420f-135">No painel de resultados, selecione **SD Elements** e, depois, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4420f-135">In the results panel, select **SD Elements**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4420f-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4420f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4420f-138">Nesta seção, você configura e testa o logon único do Azure AD com o SD Elements, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="4420f-138">In this section, you configure and test Azure AD single sign-on with SD Elements based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4420f-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do SD Elements é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4420f-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SD Elements is to a user in Azure AD.</span></span> <span data-ttu-id="4420f-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do SD Elements.</span><span class="sxs-lookup"><span data-stu-id="4420f-140">In other words, a link relationship between an Azure AD user and the related user in SD Elements needs to be established.</span></span>

<span data-ttu-id="4420f-141">No SD Elements, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="4420f-141">In SD Elements, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="4420f-142">Para configurar e testar o logon único do Azure AD com o SD Elements, é preciso concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="4420f-142">To configure and test Azure AD single sign-on with SD Elements, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="4420f-143">**[Configuração do logon único do AD do Azure](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="4420f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="4420f-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="4420f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4420f-145">**[Criando um usuário de teste do SD Elements](#creating-a-sd-elements-test-user)** – para ter um equivalente de Brenda Fernandes no SD Elements que esteja vinculado à representação de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4420f-145">**[Creating a SD Elements test user](#creating-a-sd-elements-test-user)** - to have a counterpart of Britta Simon in SD Elements that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="4420f-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="4420f-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4420f-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="4420f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4420f-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="4420f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4420f-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo SD Elements.</span><span class="sxs-lookup"><span data-stu-id="4420f-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SD Elements application.</span></span>

<span data-ttu-id="4420f-150">**Para configurar o logon único do Azure AD com o SD Elements, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="4420f-150">**To configure Azure AD single sign-on with SD Elements, perform the following steps:**</span></span>

1. <span data-ttu-id="4420f-151">No portal do Azure, na página de integração do aplicativo **SD Elements**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="4420f-151">In the Azure portal, on the **SD Elements** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="4420f-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="4420f-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_samlbase.png)

3. <span data-ttu-id="4420f-155">Na seção **Domínio e URLs do SD Elements**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="4420f-155">On the **SD Elements Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_url.png)

    <span data-ttu-id="4420f-157">a.</span><span class="sxs-lookup"><span data-stu-id="4420f-157">a.</span></span> <span data-ttu-id="4420f-158">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<tenantname>.sdelements.com/sso/saml2/metadata`</span><span class="sxs-lookup"><span data-stu-id="4420f-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<tenantname>.sdelements.com/sso/saml2/metadata`</span></span>

    <span data-ttu-id="4420f-159">b.</span><span class="sxs-lookup"><span data-stu-id="4420f-159">b.</span></span> <span data-ttu-id="4420f-160">Na caixa de texto **URL de resposta**, digite uma URL no seguinte padrão: `https://<tenantname>.sdelements.com/sso/saml2/acs/`</span><span class="sxs-lookup"><span data-stu-id="4420f-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<tenantname>.sdelements.com/sso/saml2/acs/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4420f-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="4420f-161">These values are not real.</span></span> <span data-ttu-id="4420f-162">Atualize esses valores com o Identificador e a URL de Resposta reais.</span><span class="sxs-lookup"><span data-stu-id="4420f-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="4420f-163">Contate a [equipe de suporte do SD Elements](mailto:support@sdelements.com) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="4420f-163">Contact [SD Elements support team](mailto:support@sdelements.com) to get these values.</span></span>

4. <span data-ttu-id="4420f-164">O aplicativo SD Elements espera que as declarações SAML estejam em um formato específico.</span><span class="sxs-lookup"><span data-stu-id="4420f-164">SD Elements application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="4420f-165">Configure as declarações a seguir para este aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4420f-165">Configure the following claims for this application.</span></span> <span data-ttu-id="4420f-166">Gerencie os valores desses atributos na guia “**Atributo de Usuário**” do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4420f-166">You can manage the values of these attributes from the **"User Attribute"** tab of the application.</span></span> <span data-ttu-id="4420f-167">A captura de tela a seguir mostra um exemplo disso.</span><span class="sxs-lookup"><span data-stu-id="4420f-167">The following screenshot shows an example for this.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_attribute.png)

5. <span data-ttu-id="4420f-169">Na seção **Atributos do Usuário**, na caixa de diálogo **Logon único**, configure o atributo do token SAML como mostra a imagem e execute as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="4420f-169">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span> 

    | <span data-ttu-id="4420f-170">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="4420f-170">Attribute Name</span></span> | <span data-ttu-id="4420f-171">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="4420f-171">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="4420f-172">email</span><span class="sxs-lookup"><span data-stu-id="4420f-172">email</span></span> |<span data-ttu-id="4420f-173">user.mail</span><span class="sxs-lookup"><span data-stu-id="4420f-173">user.mail</span></span> |
    | <span data-ttu-id="4420f-174">nome</span><span class="sxs-lookup"><span data-stu-id="4420f-174">firstname</span></span> |<span data-ttu-id="4420f-175">user.givenname</span><span class="sxs-lookup"><span data-stu-id="4420f-175">user.givenname</span></span> |
    | <span data-ttu-id="4420f-176">sobrenome</span><span class="sxs-lookup"><span data-stu-id="4420f-176">lastname</span></span> |<span data-ttu-id="4420f-177">user.surname</span><span class="sxs-lookup"><span data-stu-id="4420f-177">user.surname</span></span> |

    <span data-ttu-id="4420f-178">a.</span><span class="sxs-lookup"><span data-stu-id="4420f-178">a.</span></span> <span data-ttu-id="4420f-179">Clique em **Adicionar atributo** para abrir o diálogo **Adicionar Atributo**.</span><span class="sxs-lookup"><span data-stu-id="4420f-179">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-sd-elements-tutorial/tutorial_officespace_04.png)

    ![Configurar Logon Único](./media/active-directory-saas-sd-elements-tutorial/tutorial_officespace_05.png)

    <span data-ttu-id="4420f-182">b.</span><span class="sxs-lookup"><span data-stu-id="4420f-182">b.</span></span> <span data-ttu-id="4420f-183">Na caixa de texto **Nome** , digite o nome do atributo mostrado para essa linha.</span><span class="sxs-lookup"><span data-stu-id="4420f-183">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="4420f-184">c.</span><span class="sxs-lookup"><span data-stu-id="4420f-184">c.</span></span> <span data-ttu-id="4420f-185">Na lista **Valor**, digite o valor do atributo mostrado para essa linha.</span><span class="sxs-lookup"><span data-stu-id="4420f-185">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="4420f-186">d.</span><span class="sxs-lookup"><span data-stu-id="4420f-186">d.</span></span> <span data-ttu-id="4420f-187">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="4420f-187">Click **Ok**.</span></span>
 
6. <span data-ttu-id="4420f-188">Na seção **Certificado de Autenticação SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado em seu computador.</span><span class="sxs-lookup"><span data-stu-id="4420f-188">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_certificate.png) 

7. <span data-ttu-id="4420f-190">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="4420f-190">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-sd-elements-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="4420f-192">Na seção **Configuração do SD Elements**, clique em **Configurar o SD Elements** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="4420f-192">On the **SD Elements Configuration** section, click **Configure SD Elements** to open **Configure sign-on** window.</span></span> <span data-ttu-id="4420f-193">Copie a **ID da Entidade SAML e a URL do Serviço de Logon Único SAML** da **seção Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="4420f-193">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_configure.png)

9. <span data-ttu-id="4420f-195">Para habilitar logon único, entre em contato com a [equipe de suporte do SD Elements](mailto:support@sdelements.com) e forneça a ela o arquivo de certificado baixado.</span><span class="sxs-lookup"><span data-stu-id="4420f-195">To get single sign-on enabled, contact your [SD Elements support team](mailto:support@sdelements.com) and provide them with the downloaded certificate file.</span></span> 

10. <span data-ttu-id="4420f-196">Em outra janela do navegador, faça logon no locatário do SD Elements como administrador.</span><span class="sxs-lookup"><span data-stu-id="4420f-196">In a different browser window, sign-on to your SD Elements tenant as an administrator.</span></span>

11. <span data-ttu-id="4420f-197">No menu na parte superior, clique em **Sistema** e, depois, em **Logon Único**.</span><span class="sxs-lookup"><span data-stu-id="4420f-197">In the menu on the top, click **System**, and then **Single Sign-on**.</span></span> 
   
    ![Configurar Logon Único](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_09.png) 

12. <span data-ttu-id="4420f-199">Na caixa de diálogo **Configurações de Logon Único** , execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="4420f-199">On the **Single Sign-On Settings** dialog, perform the following steps:</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_10.png) 
   
    <span data-ttu-id="4420f-201">a.</span><span class="sxs-lookup"><span data-stu-id="4420f-201">a.</span></span> <span data-ttu-id="4420f-202">Como **Tipo de SSO**, selecione **SAML**.</span><span class="sxs-lookup"><span data-stu-id="4420f-202">As **SSO Type**, select **SAML**.</span></span>
   
    <span data-ttu-id="4420f-203">b.</span><span class="sxs-lookup"><span data-stu-id="4420f-203">b.</span></span> <span data-ttu-id="4420f-204">Na caixa de texto **ID da Entidade do Provedor de Identidade**, cole o valor da **ID da Entidade SAML** copiado do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="4420f-204">In the **Identity Provider Entity ID** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 
   
    <span data-ttu-id="4420f-205">c.</span><span class="sxs-lookup"><span data-stu-id="4420f-205">c.</span></span> <span data-ttu-id="4420f-206">Na caixa de texto **Serviço de Logon Único do Provedor de Identidade**, cole o valor da **URL do Serviço de Logon Único SAML** copiado do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="4420f-206">In the **Identity Provider Single Sign-On Service** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span> 
   
    <span data-ttu-id="4420f-207">d.</span><span class="sxs-lookup"><span data-stu-id="4420f-207">d.</span></span> <span data-ttu-id="4420f-208">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="4420f-208">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="4420f-209">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="4420f-209">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="4420f-210">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="4420f-210">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="4420f-211">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4420f-211">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4420f-212">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4420f-212">Creating an Azure AD test user</span></span>
<span data-ttu-id="4420f-213">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="4420f-213">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="4420f-215">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="4420f-215">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="4420f-216">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4420f-216">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sd-elements-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4420f-218">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="4420f-218">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sd-elements-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4420f-220">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4420f-220">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sd-elements-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4420f-222">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="4420f-222">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-sd-elements-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4420f-224">a.</span><span class="sxs-lookup"><span data-stu-id="4420f-224">a.</span></span> <span data-ttu-id="4420f-225">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="4420f-225">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4420f-226">b.</span><span class="sxs-lookup"><span data-stu-id="4420f-226">b.</span></span> <span data-ttu-id="4420f-227">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="4420f-227">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4420f-228">c.</span><span class="sxs-lookup"><span data-stu-id="4420f-228">c.</span></span> <span data-ttu-id="4420f-229">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="4420f-229">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="4420f-230">d.</span><span class="sxs-lookup"><span data-stu-id="4420f-230">d.</span></span> <span data-ttu-id="4420f-231">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="4420f-231">Click **Create**.</span></span>
 
### <a name="creating-a-sd-elements-test-user"></a><span data-ttu-id="4420f-232">Criar um usuário de teste de elementos de SD</span><span class="sxs-lookup"><span data-stu-id="4420f-232">Creating a SD Elements test user</span></span>

<span data-ttu-id="4420f-233">O objetivo desta seção é criar um usuário chamado Brenda Fernandes no SD Elements.</span><span class="sxs-lookup"><span data-stu-id="4420f-233">The objective of this section is to create a user called Britta Simon in SD Elements.</span></span> <span data-ttu-id="4420f-234">No caso de SD Elements, criar usuários do SD Elements é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="4420f-234">In the case of SD Elements, creating SD Elements users is a manual task.</span></span>

<span data-ttu-id="4420f-235">**Para criar Brenda Fernandes no SD Elements, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="4420f-235">**To create Britta Simon in SD Elements, perform the following steps:**</span></span>

1. <span data-ttu-id="4420f-236">Em uma janela de navegador da web, faça logon no site SD Elements da sua empresa como administrador.</span><span class="sxs-lookup"><span data-stu-id="4420f-236">In a web browser window, sign-on to your SD Elements company site as an administrator.</span></span>

2. <span data-ttu-id="4420f-237">No menu na parte superior, clique em **Gerenciamento de Usuários** e, depois, em **Usuários**.</span><span class="sxs-lookup"><span data-stu-id="4420f-237">In the menu on the top, click **User Management**, and then **Users**.</span></span>
   
    ![Criar um usuário de teste de elementos de SD](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_11.png) 

3. <span data-ttu-id="4420f-239">Clique em **Adicionar Novo Usuário**.</span><span class="sxs-lookup"><span data-stu-id="4420f-239">Click **Add New User**.</span></span>
   
    ![Criar um usuário de teste de elementos de SD](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_12.png)
 
4. <span data-ttu-id="4420f-241">Na caixa de diálogo **Adicionar Novo Usuário**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="4420f-241">On the **Add New User** dialog, perform the following steps:</span></span>
   
    ![Criar um usuário de teste de elementos de SD](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_13.png) 
   
    <span data-ttu-id="4420f-243">a.</span><span class="sxs-lookup"><span data-stu-id="4420f-243">a.</span></span> <span data-ttu-id="4420f-244">Na caixa de texto **Email**, insira o email do usuário, como **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="4420f-244">In the **E-mail** textbox, enter the email of user like **brittasimon@contoso.com**.</span></span>
   
    <span data-ttu-id="4420f-245">b.</span><span class="sxs-lookup"><span data-stu-id="4420f-245">b.</span></span> <span data-ttu-id="4420f-246">Na caixa de texto **Nome**, digite o nome do usuário, como **Brenda**.</span><span class="sxs-lookup"><span data-stu-id="4420f-246">In the **First Name** textbox, enter the first name of user like **Britta**.</span></span>
   
    <span data-ttu-id="4420f-247">c.</span><span class="sxs-lookup"><span data-stu-id="4420f-247">c.</span></span> <span data-ttu-id="4420f-248">Na caixa de texto **Sobrenome**, digite o sobrenome do usuário como **Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="4420f-248">In the **Last Name** textbox, enter the last name of user like **Simon**.</span></span>
   
    <span data-ttu-id="4420f-249">d.</span><span class="sxs-lookup"><span data-stu-id="4420f-249">d.</span></span> <span data-ttu-id="4420f-250">Como **Função**, selecione **Usuário**.</span><span class="sxs-lookup"><span data-stu-id="4420f-250">As **Role**, select **User**.</span></span> 
   
    <span data-ttu-id="4420f-251">e.</span><span class="sxs-lookup"><span data-stu-id="4420f-251">e.</span></span> <span data-ttu-id="4420f-252">Clique em **Criar Usuário**.</span><span class="sxs-lookup"><span data-stu-id="4420f-252">Click **Create User**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="4420f-253">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4420f-253">Assigning the Azure AD test user</span></span>

<span data-ttu-id="4420f-254">Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo acesso ao SD Elements.</span><span class="sxs-lookup"><span data-stu-id="4420f-254">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SD Elements.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="4420f-256">**Para atribuir Brenda Fernandes ao SD Elements, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="4420f-256">**To assign Britta Simon to SD Elements, perform the following steps:**</span></span>

1. <span data-ttu-id="4420f-257">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="4420f-257">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="4420f-259">Na lista de aplicativos, selecione **SD Elements**.</span><span class="sxs-lookup"><span data-stu-id="4420f-259">In the applications list, select **SD Elements**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_app.png) 

3. <span data-ttu-id="4420f-261">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="4420f-261">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="4420f-263">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="4420f-263">Click **Add** button.</span></span> <span data-ttu-id="4420f-264">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4420f-264">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="4420f-266">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="4420f-266">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="4420f-267">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4420f-267">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4420f-268">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4420f-268">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4420f-269">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="4420f-269">Testing single sign-on</span></span>

<span data-ttu-id="4420f-270">O objetivo desta seção é testar sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="4420f-270">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>
  
<span data-ttu-id="4420f-271">Quando você clica no bloco SD Elements no Painel de Acesso, deve fazer logon automaticamente no seu aplicativo SD Elements.</span><span class="sxs-lookup"><span data-stu-id="4420f-271">When you click the SD Elements tile in the Access Panel, you should get automatically signed-on to your SD Elements application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4420f-272">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="4420f-272">Additional resources</span></span>

* [<span data-ttu-id="4420f-273">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="4420f-273">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4420f-274">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4420f-274">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_203.png

