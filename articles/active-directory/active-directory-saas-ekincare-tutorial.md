---
title: "Tutorial: Integração do Azure Active Directory com o eKincare | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o eKincare."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 57f56d14-83cf-4cbb-b342-fac4fc60078f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: 014eaff14974bb6cd551b6fe53409ede6a6dfea1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ekincare"></a><span data-ttu-id="14578-103">Tutorial: Integração do Azure Active Directory com o eKincare</span><span class="sxs-lookup"><span data-stu-id="14578-103">Tutorial: Azure Active Directory integration with eKincare</span></span>

<span data-ttu-id="14578-104">Neste tutorial, você aprenderá a integrar o eKincare ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="14578-104">In this tutorial, you learn how to integrate eKincare with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="14578-105">A integração do eKincare ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="14578-105">Integrating eKincare with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="14578-106">No Azure AD, você pode controlar quem tem acesso ao eKincare</span><span class="sxs-lookup"><span data-stu-id="14578-106">You can control in Azure AD who has access to eKincare</span></span>
- <span data-ttu-id="14578-107">Você pode permitir que seus usuários façam logon automaticamente no eKincare (logon único) com as contas do Azure AD deles</span><span class="sxs-lookup"><span data-stu-id="14578-107">You can enable your users to automatically get signed-on to eKincare (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="14578-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="14578-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="14578-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="14578-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="14578-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="14578-110">Prerequisites</span></span>

<span data-ttu-id="14578-111">Para configurar a integração do Azure AD ao eKincare, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="14578-111">To configure Azure AD integration with eKincare, you need the following items:</span></span>

- <span data-ttu-id="14578-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="14578-112">An Azure AD subscription</span></span>
- <span data-ttu-id="14578-113">Uma assinatura do eKincare com logon único habilitado</span><span class="sxs-lookup"><span data-stu-id="14578-113">A eKincare single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="14578-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="14578-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="14578-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="14578-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="14578-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="14578-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="14578-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="14578-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="14578-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="14578-118">Scenario description</span></span>
<span data-ttu-id="14578-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="14578-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="14578-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="14578-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="14578-121">Adição do eKincare da galeria</span><span class="sxs-lookup"><span data-stu-id="14578-121">Adding eKincare from the gallery</span></span>
2. <span data-ttu-id="14578-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="14578-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ekincare-from-the-gallery"></a><span data-ttu-id="14578-123">Adição do eKincare da galeria</span><span class="sxs-lookup"><span data-stu-id="14578-123">Adding eKincare from the gallery</span></span>
<span data-ttu-id="14578-124">Para configurar a integração do eKincare com o Azure AD, você precisa adicionar o eKincare à sua lista de aplicativos SaaS gerenciados a partir da galeria.</span><span class="sxs-lookup"><span data-stu-id="14578-124">To configure the integration of eKincare into Azure AD, you need to add eKincare from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="14578-125">**Para adicionar o eKincare a partir da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="14578-125">**To add eKincare from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="14578-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="14578-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="14578-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="14578-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="14578-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="14578-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="14578-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="14578-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="14578-133">Na caixa de pesquisa, digite **eKincare**.</span><span class="sxs-lookup"><span data-stu-id="14578-133">In the search box, type **eKincare**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_search.png)

5. <span data-ttu-id="14578-135">No painel de resultados, selecione **eKincare** e clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="14578-135">In the results panel, select **eKincare**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="14578-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="14578-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="14578-138">Nesta seção, você configurará e testará o logon único do Azure AD com o eKincare, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="14578-138">In this section, you configure and test Azure AD single sign-on with eKincare based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="14578-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do eKincare é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="14578-139">For single sign-on to work, Azure AD needs to know what the counterpart user in eKincare is to a user in Azure AD.</span></span> <span data-ttu-id="14578-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado no eKincare.</span><span class="sxs-lookup"><span data-stu-id="14578-140">In other words, a link relationship between an Azure AD user and the related user in eKincare needs to be established.</span></span>

<span data-ttu-id="14578-141">No eKincare, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="14578-141">In eKincare, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="14578-142">Para configurar e testar o logon único do Azure AD com o eKincare, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="14578-142">To configure and test Azure AD single sign-on with eKincare, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="14578-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="14578-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="14578-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="14578-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="14578-145">**[Criação de um usuário de teste do eKincare](#creating-a-ekincare-test-user)** – para ter um equivalente de Brenda Fernandes no eKincare que esteja vinculado à representação do usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="14578-145">**[Creating a eKincare test user](#creating-a-ekincare-test-user)** - to have a counterpart of Britta Simon in eKincare that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="14578-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="14578-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="14578-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="14578-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="14578-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="14578-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="14578-149">Nesta seção, você habilita o logon único do Azure AD no Portal do Azure e configura o logon único no aplicativo eKincare.</span><span class="sxs-lookup"><span data-stu-id="14578-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your eKincare application.</span></span>

<span data-ttu-id="14578-150">**Para configurar o logon único do Azure AD com o eKincare, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="14578-150">**To configure Azure AD single sign-on with eKincare, perform the following steps:**</span></span>

1. <span data-ttu-id="14578-151">No Portal do Azure, na página de integração de aplicativos do **eKincare**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="14578-151">In the Azure portal, on the **eKincare** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="14578-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="14578-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_samlbase.png)

3. <span data-ttu-id="14578-155">Na seção **URLs e Domínio do eKincare**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="14578-155">On the **eKincare Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_url.png)

    <span data-ttu-id="14578-157">a.</span><span class="sxs-lookup"><span data-stu-id="14578-157">a.</span></span> <span data-ttu-id="14578-158">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<instancename>.ekincare.com/`</span><span class="sxs-lookup"><span data-stu-id="14578-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<instancename>.ekincare.com/`</span></span>

    <span data-ttu-id="14578-159">b.</span><span class="sxs-lookup"><span data-stu-id="14578-159">b.</span></span> <span data-ttu-id="14578-160">Na caixa de texto **URL de resposta**, digite uma URL no seguinte padrão: `https://<instancename>.ekincare.com/hul/saml`</span><span class="sxs-lookup"><span data-stu-id="14578-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<instancename>.ekincare.com/hul/saml`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="14578-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="14578-161">These values are not real.</span></span> <span data-ttu-id="14578-162">Atualize esses valores com o Identificador e a URL de Resposta reais.</span><span class="sxs-lookup"><span data-stu-id="14578-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="14578-163">Entre em contato com a [equipe de suporte do eKincare](mailto:tech@ekincare.com) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="14578-163">Contact [eKincare support team](mailto:tech@ekincare.com) to get these values.</span></span>
 
4. <span data-ttu-id="14578-164">O aplicativo eKincare espera que as declarações SAML estejam em um formato específico.</span><span class="sxs-lookup"><span data-stu-id="14578-164">eKincare application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="14578-165">Configure as declarações a seguir para este aplicativo.</span><span class="sxs-lookup"><span data-stu-id="14578-165">Configure the following claims for this application.</span></span> <span data-ttu-id="14578-166">Você pode gerenciar os valores desses atributos da seção "**Atributos de Usuário**" na página de integração do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="14578-166">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="14578-167">A captura de tela a seguir mostra um exemplo dessa configuração.</span><span class="sxs-lookup"><span data-stu-id="14578-167">The following screenshot shows an example for this configuration.</span></span>

    <span data-ttu-id="14578-168">O nome da declaração sempre será **"employeeid"** e o valor dela foi mapeado para user.extensionattribute1, que contém a employeeid do usuário.</span><span class="sxs-lookup"><span data-stu-id="14578-168">The claim name will always be **"employeeid"** and the value of which we have mapped to user.extensionattribute1, that contains the employeeid of the user.</span></span> <span data-ttu-id="14578-169">O nome das outras duas declarações, ou seja,</span><span class="sxs-lookup"><span data-stu-id="14578-169">The other two claims' name i.e</span></span> <span data-ttu-id="14578-170">**"organizationid"** e **"organizationname"** não mudam e seus valores contêm os detalhes da organização e do usuário, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="14578-170">**"organizationid"** and **"organizationname"** will always be same and their values contain the details of the organization of the user respectively.</span></span>
    
    ![Configurar Logon Único](./media/active-directory-saas-ekincare-tutorial/attribute.png)
    
5. <span data-ttu-id="14578-172">Na seção **Atributos do usuário**, na caixa de diálogo **Logon único**, configure o atributo do token SAML na imagem acima e siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="14578-172">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>
    
    | <span data-ttu-id="14578-173">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="14578-173">Attribute Name</span></span> | <span data-ttu-id="14578-174">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="14578-174">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="14578-175">employeeid</span><span class="sxs-lookup"><span data-stu-id="14578-175">employeeid</span></span> | <span data-ttu-id="14578-176">*user.extensionattribute1*</span><span class="sxs-lookup"><span data-stu-id="14578-176">*user.extensionattribute1*</span></span> |
    | <span data-ttu-id="14578-177">organizationid</span><span class="sxs-lookup"><span data-stu-id="14578-177">organizationid</span></span> | <span data-ttu-id="14578-178">*"uniquevalue"*</span><span class="sxs-lookup"><span data-stu-id="14578-178">*"uniquevalue"*</span></span> |
    | <span data-ttu-id="14578-179">organizationname</span><span class="sxs-lookup"><span data-stu-id="14578-179">organizationname</span></span> | <span data-ttu-id="14578-180">*user.companyname*</span><span class="sxs-lookup"><span data-stu-id="14578-180">*user.companyname*</span></span> |

    <span data-ttu-id="14578-181">a.</span><span class="sxs-lookup"><span data-stu-id="14578-181">a.</span></span> <span data-ttu-id="14578-182">Clique em **Adicionar atributo** para abrir o diálogo **Adicionar Atributo**.</span><span class="sxs-lookup"><span data-stu-id="14578-182">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-ekincare-tutorial/04.png)

    ![Configurar Logon Único](./media/active-directory-saas-ekincare-tutorial/05.png)
    
    <span data-ttu-id="14578-185">b.</span><span class="sxs-lookup"><span data-stu-id="14578-185">b.</span></span> <span data-ttu-id="14578-186">Na caixa de texto **Nome** , digite o nome do atributo mostrado para essa linha.</span><span class="sxs-lookup"><span data-stu-id="14578-186">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="14578-187">c.</span><span class="sxs-lookup"><span data-stu-id="14578-187">c.</span></span> <span data-ttu-id="14578-188">Na lista **Valor**, digite o valor do atributo mostrado para essa linha.</span><span class="sxs-lookup"><span data-stu-id="14578-188">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="14578-189">d.</span><span class="sxs-lookup"><span data-stu-id="14578-189">d.</span></span> <span data-ttu-id="14578-190">Clique em **Ok**</span><span class="sxs-lookup"><span data-stu-id="14578-190">Click **Ok**</span></span>

6. <span data-ttu-id="14578-191">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="14578-191">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_certificate.png) 

7. <span data-ttu-id="14578-193">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="14578-193">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-ekincare-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="14578-195">Para configurar o logon único no lado do **eKincare**, é necessário enviar o **XML de metadados** baixado para a [equipe de suporte do eKincare](mailto:tech@ekincare.com).</span><span class="sxs-lookup"><span data-stu-id="14578-195">To configure single sign-on on **eKincare** side, you need to send the downloaded **Metadata XML** to [eKincare support team](mailto:tech@ekincare.com).</span></span> <span data-ttu-id="14578-196">Eles definem essa configuração para ter a conexão de SSO do SAML definida corretamente em ambos os lados.</span><span class="sxs-lookup"><span data-stu-id="14578-196">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="14578-197">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="14578-197">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="14578-198">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="14578-198">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="14578-199">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="14578-199">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="14578-200">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="14578-200">Creating an Azure AD test user</span></span>
<span data-ttu-id="14578-201">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="14578-201">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="14578-203">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="14578-203">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="14578-204">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="14578-204">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-ekincare-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="14578-206">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="14578-206">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-ekincare-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="14578-208">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="14578-208">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-ekincare-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="14578-210">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="14578-210">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-ekincare-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="14578-212">a.</span><span class="sxs-lookup"><span data-stu-id="14578-212">a.</span></span> <span data-ttu-id="14578-213">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="14578-213">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="14578-214">b.</span><span class="sxs-lookup"><span data-stu-id="14578-214">b.</span></span> <span data-ttu-id="14578-215">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="14578-215">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="14578-216">c.</span><span class="sxs-lookup"><span data-stu-id="14578-216">c.</span></span> <span data-ttu-id="14578-217">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="14578-217">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="14578-218">d.</span><span class="sxs-lookup"><span data-stu-id="14578-218">d.</span></span> <span data-ttu-id="14578-219">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="14578-219">Click **Create**.</span></span>
 
### <a name="creating-a-ekincare-test-user"></a><span data-ttu-id="14578-220">Criar um usuário de teste do eKincare</span><span class="sxs-lookup"><span data-stu-id="14578-220">Creating a eKincare test user</span></span>

<span data-ttu-id="14578-221">O aplicativo dá suporte ao provisionamento de usuário Just-In-Time e, após a autenticação, os usuários são criados no aplicativo automaticamente.</span><span class="sxs-lookup"><span data-stu-id="14578-221">Application supports Just in time user provisioning and after authentication users are created in the application automatically.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="14578-222">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="14578-222">Assigning the Azure AD test user</span></span>

<span data-ttu-id="14578-223">Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao eKincare.</span><span class="sxs-lookup"><span data-stu-id="14578-223">In this section, you enable Britta Simon to use Azure single sign-on by granting access to eKincare.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="14578-225">**Para atribuir Brenda Fernandes ao eKincare, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="14578-225">**To assign Britta Simon to eKincare, perform the following steps:**</span></span>

1. <span data-ttu-id="14578-226">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="14578-226">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="14578-228">Na lista de aplicativos, escolha **eKincare**.</span><span class="sxs-lookup"><span data-stu-id="14578-228">In the applications list, select **eKincare**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_app.png) 

3. <span data-ttu-id="14578-230">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="14578-230">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="14578-232">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="14578-232">Click **Add** button.</span></span> <span data-ttu-id="14578-233">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="14578-233">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="14578-235">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="14578-235">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="14578-236">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="14578-236">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="14578-237">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="14578-237">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="14578-238">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="14578-238">Testing single sign-on</span></span>

<span data-ttu-id="14578-239">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="14578-239">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="14578-240">Ao clicar no bloco do eKincare no Painel de Acesso, você deverá ser conectado automaticamente ao seu aplicativo eKincare.</span><span class="sxs-lookup"><span data-stu-id="14578-240">When you click the eKincare tile in the Access Panel, you should get automatically signed-on to your eKincare application.</span></span>
<span data-ttu-id="14578-241">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="14578-241">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md)</span></span>

## <a name="additional-resources"></a><span data-ttu-id="14578-242">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="14578-242">Additional resources</span></span>

* [<span data-ttu-id="14578-243">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="14578-243">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="14578-244">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="14578-244">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_203.png

