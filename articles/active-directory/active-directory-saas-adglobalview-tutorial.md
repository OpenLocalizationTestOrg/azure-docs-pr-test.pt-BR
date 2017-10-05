---
title: "Tutorial: Integração do Azure Active Directory ao ADP Globalview | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o ADP Globalview."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ffb6464f-714d-41a9-869a-2b7e5ae9f125
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: e9a5e65c484dfb98d1a7bc63d55f6ef92039554b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adp-globalview"></a><span data-ttu-id="cdde4-103">Tutorial: Integração do Azure Active Directory ao ADP Globalview</span><span class="sxs-lookup"><span data-stu-id="cdde4-103">Tutorial: Azure Active Directory integration with ADP Globalview</span></span>

<span data-ttu-id="cdde4-104">Neste tutorial, você aprende a integrar o ADP Globalview ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="cdde4-104">In this tutorial, you learn how to integrate ADP Globalview with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cdde4-105">A integração do ADP Globalview ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="cdde4-105">Integrating ADP Globalview with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="cdde4-106">No Azure AD, é possível controlar quem tem acesso ao ADP Globalview</span><span class="sxs-lookup"><span data-stu-id="cdde4-106">You can control in Azure AD who has access to ADP Globalview</span></span>
- <span data-ttu-id="cdde4-107">É possível permitir que os usuários se conectem automaticamente ao ADP Globalview (Logon Único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="cdde4-107">You can enable your users to automatically get signed-on to ADP Globalview (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="cdde4-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="cdde4-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="cdde4-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="cdde4-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cdde4-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="cdde4-110">Prerequisites</span></span>

<span data-ttu-id="cdde4-111">Para configurar a integração do Azure AD ao ADP Globalview, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="cdde4-111">To configure Azure AD integration with ADP Globalview, you need the following items:</span></span>

- <span data-ttu-id="cdde4-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="cdde4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cdde4-113">Uma assinatura habilitada para logon único do ADP Globalview</span><span class="sxs-lookup"><span data-stu-id="cdde4-113">An ADP Globalview single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cdde4-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="cdde4-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cdde4-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="cdde4-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cdde4-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="cdde4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cdde4-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cdde4-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cdde4-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="cdde4-118">Scenario description</span></span>
<span data-ttu-id="cdde4-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="cdde4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cdde4-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="cdde4-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cdde4-121">Adicionando o ADP Globalview por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="cdde4-121">Adding ADP Globalview from the gallery</span></span>
2. <span data-ttu-id="cdde4-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="cdde4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adp-globalview-from-the-gallery"></a><span data-ttu-id="cdde4-123">Adicionando o ADP Globalview por meio da galeria</span><span class="sxs-lookup"><span data-stu-id="cdde4-123">Adding ADP Globalview from the gallery</span></span>
<span data-ttu-id="cdde4-124">Para configurar a integração do ADP Globalview ao Azure AD, você precisa adicionar o ADP Globalview à lista de aplicativos SaaS gerenciados por meio da galeria.</span><span class="sxs-lookup"><span data-stu-id="cdde4-124">To configure the integration of ADP Globalview into Azure AD, you need to add ADP Globalview from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="cdde4-125">**Para adicionar o ADP Globalview por meio da galeria, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="cdde4-125">**To add ADP Globalview from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="cdde4-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="cdde4-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="cdde4-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="cdde4-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="cdde4-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="cdde4-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="cdde4-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="cdde4-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="cdde4-133">Na caixa de pesquisa, digite **ADP Globalview**.</span><span class="sxs-lookup"><span data-stu-id="cdde4-133">In the search box, type **ADP Globalview**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_search.png)

5. <span data-ttu-id="cdde4-135">No painel de resultados, selecione **ADP Globalview** e, depois, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="cdde4-135">In the results panel, select **ADP Globalview**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="cdde4-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="cdde4-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="cdde4-138">Nesta seção, você configurará e testará o logon único do Azure AD com o ADP Globalview, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="cdde4-138">In this section, you configure and test Azure AD single sign-on with ADP Globalview based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="cdde4-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do ADP Globalview é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cdde4-139">For single sign-on to work, Azure AD needs to know what the counterpart user in ADP Globalview is to a user in Azure AD.</span></span> <span data-ttu-id="cdde4-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do ADP Globalview.</span><span class="sxs-lookup"><span data-stu-id="cdde4-140">In other words, a link relationship between an Azure AD user and the related user in ADP Globalview needs to be established.</span></span>

<span data-ttu-id="cdde4-141">Essa relação de vínculo é estabelecida por meio da atribuição do valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** no ADP Globalview.</span><span class="sxs-lookup"><span data-stu-id="cdde4-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ADP Globalview.</span></span>

<span data-ttu-id="cdde4-142">Para configurar e testar o logon único do Azure AD com o ADP Globalview, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="cdde4-142">To configure and test Azure AD single sign-on with ADP Globalview, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="cdde4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="cdde4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="cdde4-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="cdde4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cdde4-145">**[Criando um usuário de teste do ADP Globalview](#creating-an-adp-globalview-test-user)** – para ter um equivalente de Brenda Fernandes no ADP Globalview que esteja vinculado à representação de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cdde4-145">**[Creating an ADP Globalview test user](#creating-an-adp-globalview-test-user)** - to have a counterpart of Britta Simon in ADP Globalview that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="cdde4-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="cdde4-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cdde4-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="cdde4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="cdde4-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="cdde4-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="cdde4-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo ADP Globalview.</span><span class="sxs-lookup"><span data-stu-id="cdde4-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ADP Globalview application.</span></span>

<span data-ttu-id="cdde4-150">**Para configurar o logon único do Azure AD com o ADP Globalview, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="cdde4-150">**To configure Azure AD single sign-on with ADP Globalview, perform the following steps:**</span></span>

1. <span data-ttu-id="cdde4-151">No portal do Azure, na página de integração do aplicativo do **ADP Globalview**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="cdde4-151">In the Azure portal, on the **ADP Globalview** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="cdde4-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="cdde4-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_samlbase.png)

3. <span data-ttu-id="cdde4-155">Na seção **Domínio e URLs do ADP Globalview**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="cdde4-155">On the **ADP Globalview Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_url.png)

     <span data-ttu-id="cdde4-157">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<subdomain>.globalview.adp.com/federate` ou `https://<subdomain>.globalview.adp.com/federate2`</span><span class="sxs-lookup"><span data-stu-id="cdde4-157">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.globalview.adp.com/federate` or `https://<subdomain>.globalview.adp.com/federate2`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="cdde4-158">O valor não é real.</span><span class="sxs-lookup"><span data-stu-id="cdde4-158">The value is not real.</span></span> <span data-ttu-id="cdde4-159">Atualize o valor com o identificador real.</span><span class="sxs-lookup"><span data-stu-id="cdde4-159">Update the value with the actual Identifier.</span></span> <span data-ttu-id="cdde4-160">Contate o [suporte do ADP Globalview](https://www.adp.com/contact-us/overview.aspx) para obter o valor.</span><span class="sxs-lookup"><span data-stu-id="cdde4-160">Contact [ADP Globalview support](https://www.adp.com/contact-us/overview.aspx) to get the value.</span></span>
 
4. <span data-ttu-id="cdde4-161">Na seção **Certificado de Autenticação SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado em seu computador.</span><span class="sxs-lookup"><span data-stu-id="cdde4-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_certificate.png) 

5. <span data-ttu-id="cdde4-163">O aplicativo ADP GlobalView espera as declarações do SAML em um formato específico, o que exige a adição de mapeamentos de atributo personalizados para a configuração de atributos do token SAML.</span><span class="sxs-lookup"><span data-stu-id="cdde4-163">The ADP GlobalView application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> 

6. <span data-ttu-id="cdde4-164">A captura de tela a seguir mostra um exemplo disso.</span><span class="sxs-lookup"><span data-stu-id="cdde4-164">The following screenshot shows an example for it.</span></span> <span data-ttu-id="cdde4-165">Os nomes da declaração sempre serão **“PersonImmutableID”** e o valor que mapeamos para ExtensionAttribute2, que contém a EmployeeID do usuário.</span><span class="sxs-lookup"><span data-stu-id="cdde4-165">The claim names always be **"PersonImmutableID"** and the value of which we have mapped to ExtensionAttribute2, which contains the EmployeeID of the user.</span></span> <span data-ttu-id="cdde4-166">Aqui, o mapeamento de usuário do Azure AD para o ADP GlobalView é feito na EmployeeID, mas isso pode ser mapeado para um valor diferente também baseado nas configurações do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="cdde4-166">Here the user mapping from Azure AD to ADP GlobalView is done on the EmployeeID but you can map it to a different value also based on your application settings.</span></span> <span data-ttu-id="cdde4-167">Você pode trabalhar com a equipe do ADP GlobalView primeiro para usar o identificador correto de um usuário e mapear esse valor com a declaração **"PersonImmutableID"**.</span><span class="sxs-lookup"><span data-stu-id="cdde4-167">You can work with the ADP GlobalView team first to use the correct identifier of a user and map that value with the **"PersonImmutableID"** claim.</span></span> <span data-ttu-id="cdde4-168">Você também pode mapear a declaração de Email e ID de usuário, conforme mostra na imagem.</span><span class="sxs-lookup"><span data-stu-id="cdde4-168">You can also map the Email and UserID claim as shown in the picture.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_attribute.png)

7. <span data-ttu-id="cdde4-170">Na seção **Atributos do Usuário**, na caixa de diálogo **Logon único**, configure o atributo do token SAML como mostra a imagem e execute as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="cdde4-170">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="cdde4-171">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="cdde4-171">Attribute Name</span></span> | <span data-ttu-id="cdde4-172">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="cdde4-172">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="cdde4-173">personalimmutableid</span><span class="sxs-lookup"><span data-stu-id="cdde4-173">personalimmutableid</span></span> | <span data-ttu-id="cdde4-174">user.extensionattribute2</span><span class="sxs-lookup"><span data-stu-id="cdde4-174">user.extensionattribute2</span></span> |
    | <span data-ttu-id="cdde4-175">email</span><span class="sxs-lookup"><span data-stu-id="cdde4-175">email</span></span>               | <span data-ttu-id="cdde4-176">user.mail</span><span class="sxs-lookup"><span data-stu-id="cdde4-176">user.mail</span></span> |
    | <span data-ttu-id="cdde4-177">userid</span><span class="sxs-lookup"><span data-stu-id="cdde4-177">userid</span></span>              | <span data-ttu-id="cdde4-178">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="cdde4-178">user.userprincipalname</span></span>|
    
    <span data-ttu-id="cdde4-179">a.</span><span class="sxs-lookup"><span data-stu-id="cdde4-179">a.</span></span> <span data-ttu-id="cdde4-180">Clique em **Adicionar atributo** para abrir o diálogo **Adicionar Atributo**.</span><span class="sxs-lookup"><span data-stu-id="cdde4-180">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-adglobalview-tutorial/tutorial_attribute_04.png)

    ![Configurar Logon Único](./media/active-directory-saas-adglobalview-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="cdde4-183">b.</span><span class="sxs-lookup"><span data-stu-id="cdde4-183">b.</span></span> <span data-ttu-id="cdde4-184">Na caixa de texto **Nome** , digite o nome do atributo mostrado para essa linha.</span><span class="sxs-lookup"><span data-stu-id="cdde4-184">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="cdde4-185">c.</span><span class="sxs-lookup"><span data-stu-id="cdde4-185">c.</span></span> <span data-ttu-id="cdde4-186">Na lista **Valor**, digite o valor do atributo mostrado para essa linha.</span><span class="sxs-lookup"><span data-stu-id="cdde4-186">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="cdde4-187">d.</span><span class="sxs-lookup"><span data-stu-id="cdde4-187">d.</span></span> <span data-ttu-id="cdde4-188">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="cdde4-188">Click **Ok**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="cdde4-189">Antes de configurar a declaração SAML, você precisa contatar o [suporte do ADP Globalview](https://www.adp.com/contact-us/overview.aspx) e solicitar o valor do atributo de identificador exclusivo para seu locatário.</span><span class="sxs-lookup"><span data-stu-id="cdde4-189">Before you can configure the SAML assertion, you need to contact your [ADP Globalview support](https://www.adp.com/contact-us/overview.aspx) and request the value of the unique identifier attribute for your tenant.</span></span> <span data-ttu-id="cdde4-190">Você precisa desse valor para configurar a declaração personalizada para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="cdde4-190">You need this value to configure the custom claim for your application.</span></span> 

8. <span data-ttu-id="cdde4-191">Na seção **Configuração do ADP Globalview**, clique em **Configurar o ADP Globalview** para abrir a janela **Configurar logon**.</span><span class="sxs-lookup"><span data-stu-id="cdde4-191">On the **ADP Globalview Configuration** section, click **Configure ADP Globalview** to open **Configure sign-on** window.</span></span> <span data-ttu-id="cdde4-192">Copie a **URL de saída, a ID da Entidade SAML e a URL do Serviço de Logon Único SAML** da **seção de Referência Rápida.**</span><span class="sxs-lookup"><span data-stu-id="cdde4-192">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_configure.png) 

9. <span data-ttu-id="cdde4-194">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="cdde4-194">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-adglobalview-tutorial/tutorial_general_400.png)

10. <span data-ttu-id="cdde4-196">Para configurar o logon único no lado do **ADP Globalview**, é necessário enviar o **Certificado (Base64)** baixado, a **URL de Saída, ID da Entidade SAML e URL do Serviço de Logon Único SAML** para o [suporte do ADP Globalview](https://www.adp.com/contact-us/overview.aspx).</span><span class="sxs-lookup"><span data-stu-id="cdde4-196">To configure single sign-on on **ADP Globalview** side, you need to send the downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [ADP Globalview support](https://www.adp.com/contact-us/overview.aspx).</span></span>

> [!TIP]
> <span data-ttu-id="cdde4-197">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="cdde4-197">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="cdde4-198">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="cdde4-198">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="cdde4-199">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="cdde4-199">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="cdde4-200">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="cdde4-200">Creating an Azure AD test user</span></span>
<span data-ttu-id="cdde4-201">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="cdde4-201">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="cdde4-203">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="cdde4-203">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="cdde4-204">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="cdde4-204">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-adglobalview-tutorial/create_aaduser_01.png) 

2.  <span data-ttu-id="cdde4-206">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="cdde4-206">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-adglobalview-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="cdde4-208">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="cdde4-208">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-adglobalview-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="cdde4-210">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="cdde4-210">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-adglobalview-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="cdde4-212">a.</span><span class="sxs-lookup"><span data-stu-id="cdde4-212">a.</span></span> <span data-ttu-id="cdde4-213">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="cdde4-213">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cdde4-214">b.</span><span class="sxs-lookup"><span data-stu-id="cdde4-214">b.</span></span> <span data-ttu-id="cdde4-215">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="cdde4-215">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="cdde4-216">c.</span><span class="sxs-lookup"><span data-stu-id="cdde4-216">c.</span></span> <span data-ttu-id="cdde4-217">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="cdde4-217">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="cdde4-218">d.</span><span class="sxs-lookup"><span data-stu-id="cdde4-218">d.</span></span> <span data-ttu-id="cdde4-219">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="cdde4-219">Click **Create**.</span></span>
 
### <a name="creating-an-adp-globalview-test-user"></a><span data-ttu-id="cdde4-220">Criando um usuário de teste do ADP Globalview</span><span class="sxs-lookup"><span data-stu-id="cdde4-220">Creating an ADP Globalview test user</span></span>

<span data-ttu-id="cdde4-221">O objetivo desta seção é criar um usuário chamado Brenda Fernandes no ADP GlobalView.</span><span class="sxs-lookup"><span data-stu-id="cdde4-221">The objective of this section is to create a user called Britta Simon in ADP GlobalView.</span></span> <span data-ttu-id="cdde4-222">Trabalhe com a [equipe de suporte do ADP Globalview](https://www.adp.com/contact-us/overview.aspx) para adicionar os usuários à conta do ADP GlobalView.</span><span class="sxs-lookup"><span data-stu-id="cdde4-222">Work with [ADP Globalview support](https://www.adp.com/contact-us/overview.aspx) to add the users in the ADP GlobalView account.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="cdde4-223">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="cdde4-223">Assigning the Azure AD test user</span></span>

<span data-ttu-id="cdde4-224">Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo acesso ao ADP Globalview.</span><span class="sxs-lookup"><span data-stu-id="cdde4-224">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ADP Globalview.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="cdde4-226">**Para atribuir Brenda Fernandes ao ADP Globalview, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="cdde4-226">**To assign Britta Simon to ADP Globalview, perform the following steps:**</span></span>

1. <span data-ttu-id="cdde4-227">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="cdde4-227">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="cdde4-229">Na lista de aplicativos, selecione **ADP Globalview**.</span><span class="sxs-lookup"><span data-stu-id="cdde4-229">In the applications list, select **ADP Globalview**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_app.png) 

3. <span data-ttu-id="cdde4-231">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="cdde4-231">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="cdde4-233">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="cdde4-233">Click **Add** button.</span></span> <span data-ttu-id="cdde4-234">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="cdde4-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="cdde4-236">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="cdde4-236">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="cdde4-237">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="cdde4-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="cdde4-238">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="cdde4-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="cdde4-239">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="cdde4-239">Testing single sign-on</span></span>

<span data-ttu-id="cdde4-240">O objetivo desta seção é testar sua configuração de SSO do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="cdde4-240">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>  

<span data-ttu-id="cdde4-241">Ao clicar no bloco do ADP GlobalView no Painel de Acesso, você deverá ser conectado automaticamente ao seu aplicativo do ADP GlobalView.</span><span class="sxs-lookup"><span data-stu-id="cdde4-241">When you click the ADP GlobalView tile in the Access Panel, you should get automatically signed-on to your ADP GlobalView application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="cdde4-242">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="cdde4-242">Additional resources</span></span>

* [<span data-ttu-id="cdde4-243">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="cdde4-243">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cdde4-244">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="cdde4-244">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_203.png

