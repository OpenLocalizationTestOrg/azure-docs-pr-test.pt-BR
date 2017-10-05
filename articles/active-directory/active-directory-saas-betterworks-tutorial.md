---
title: "Tutorial: Integração do Azure Active Directory ao BetterWorks | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o BetterWorks."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5bb9505a-be02-46ae-9979-5308715d2b47
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: d6a5b167c0befbd0fe2c65bdd16abc35ed0a659c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-betterworks"></a><span data-ttu-id="3bc80-103">Tutorial: integração do Azure Active Directory ao BetterWorks</span><span class="sxs-lookup"><span data-stu-id="3bc80-103">Tutorial: Azure Active Directory integration with BetterWorks</span></span>

<span data-ttu-id="3bc80-104">Neste tutorial, você aprende a integrar o BetterWorks ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="3bc80-104">In this tutorial, you learn how to integrate BetterWorks with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3bc80-105">A integração do BetterWorks ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="3bc80-105">Integrating BetterWorks with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3bc80-106">No Azure AD, você poderá controlar quem tem acesso ao BetterWorks</span><span class="sxs-lookup"><span data-stu-id="3bc80-106">You can control in Azure AD who has access to BetterWorks</span></span>
- <span data-ttu-id="3bc80-107">Você pode permitir que seus usuários façam logon automaticamente no BetterWorks (logon único) com suas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="3bc80-107">You can enable your users to automatically get signed-on to BetterWorks (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3bc80-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="3bc80-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="3bc80-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3bc80-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3bc80-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="3bc80-110">Prerequisites</span></span>

<span data-ttu-id="3bc80-111">Para configurar a integração do Azure AD ao BetterWorks, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="3bc80-111">To configure Azure AD integration with BetterWorks, you need the following items:</span></span>

- <span data-ttu-id="3bc80-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3bc80-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3bc80-113">Uma assinatura habilitada para logon único do BetterWorks</span><span class="sxs-lookup"><span data-stu-id="3bc80-113">A BetterWorks single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3bc80-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="3bc80-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3bc80-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="3bc80-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3bc80-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="3bc80-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3bc80-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3bc80-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3bc80-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="3bc80-118">Scenario description</span></span>
<span data-ttu-id="3bc80-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="3bc80-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3bc80-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="3bc80-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3bc80-121">Adicionando o BetterWorks da galeria</span><span class="sxs-lookup"><span data-stu-id="3bc80-121">Adding BetterWorks from the gallery</span></span>
2. <span data-ttu-id="3bc80-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3bc80-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-betterworks-from-the-gallery"></a><span data-ttu-id="3bc80-123">Adicionando o BetterWorks da galeria</span><span class="sxs-lookup"><span data-stu-id="3bc80-123">Adding BetterWorks from the gallery</span></span>
<span data-ttu-id="3bc80-124">Para configurar a integração do BetterWorks ao Azure AD, você precisará adicionar o BetterWorks da galeria à sua lista de aplicativos de SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="3bc80-124">To configure the integration of BetterWorks into Azure AD, you need to add BetterWorks from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3bc80-125">**Para adicionar o BetterWorks da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="3bc80-125">**To add BetterWorks from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3bc80-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3bc80-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3bc80-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="3bc80-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="3bc80-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="3bc80-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="3bc80-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3bc80-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="3bc80-133">Na caixa de pesquisa, digite **BetterWorks**.</span><span class="sxs-lookup"><span data-stu-id="3bc80-133">In the search box, type **BetterWorks**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_search.png)

5. <span data-ttu-id="3bc80-135">No painel de resultados, selecione **BetterWorks** e, depois, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3bc80-135">In the results panel, select **BetterWorks**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3bc80-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3bc80-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3bc80-138">Nesta seção, você configura e testa o logon único do Azure AD com o BetterWorks, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="3bc80-138">In this section, you configure and test Azure AD single sign-on with BetterWorks based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="3bc80-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário do BetterWorks é equivalente a um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3bc80-139">For single sign-on to work, Azure AD needs to know what the counterpart user in BetterWorks is to a user in Azure AD.</span></span> <span data-ttu-id="3bc80-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do BetterWorks.</span><span class="sxs-lookup"><span data-stu-id="3bc80-140">In other words, a link relationship between an Azure AD user and the related user in BetterWorks needs to be established.</span></span>

<span data-ttu-id="3bc80-141">No BetterWorks, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="3bc80-141">In BetterWorks, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="3bc80-142">Para configurar e testar o logon único do Azure AD com o BetterWorks, você precisará executar as seguintes tarefas básicas:</span><span class="sxs-lookup"><span data-stu-id="3bc80-142">To configure and test Azure AD single sign-on with BetterWorks, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3bc80-143">**[Configuração do logon único do AD do Azure](#configuring-azure-ad-single-sign-on)** : para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="3bc80-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3bc80-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="3bc80-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3bc80-145">**[Criando um usuário de teste do BetterWorks](#creating-a-betterworks-test-user)** – para ter um equivalente de Brenda Fernandes no BetterWorks que esteja vinculado à representação de usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3bc80-145">**[Creating a BetterWorks test user](#creating-a-betterworks-test-user)** - to have a counterpart of Britta Simon in BetterWorks that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="3bc80-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="3bc80-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3bc80-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="3bc80-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3bc80-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="3bc80-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3bc80-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo BetterWorks.</span><span class="sxs-lookup"><span data-stu-id="3bc80-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your BetterWorks application.</span></span>

<span data-ttu-id="3bc80-150">**Para configurar o logon único do Azure AD com o BetterWorks, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="3bc80-150">**To configure Azure AD single sign-on with BetterWorks, perform the following steps:**</span></span>

1. <span data-ttu-id="3bc80-151">No portal do Azure, na página de integração do aplicativo do **BetterWorks**, clique em **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="3bc80-151">In the Azure portal, on the **BetterWorks** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="3bc80-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="3bc80-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_samlbase.png)

3. <span data-ttu-id="3bc80-155">Na seção **Domínio e URLs do BetterWorks**, se desejar configurar o aplicativo no **modo iniciado pelo IDP**:</span><span class="sxs-lookup"><span data-stu-id="3bc80-155">On the **BetterWorks Domain and URLs** section, If you wish to configure the application in **IDP initiated mode**:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_url.png)

    <span data-ttu-id="3bc80-157">a.</span><span class="sxs-lookup"><span data-stu-id="3bc80-157">a.</span></span> <span data-ttu-id="3bc80-158">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://app.betterworks.com/saml2/metadata/`</span><span class="sxs-lookup"><span data-stu-id="3bc80-158">In the **Identifier** textbox, type a URL using the following pattern: `https://app.betterworks.com/saml2/metadata/`</span></span>

    <span data-ttu-id="3bc80-159">b.</span><span class="sxs-lookup"><span data-stu-id="3bc80-159">b.</span></span> <span data-ttu-id="3bc80-160">Na caixa de texto **URL de resposta**, digite uma URL no seguinte padrão: `https://app.betterworks.com/saml2/acs/`</span><span class="sxs-lookup"><span data-stu-id="3bc80-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://app.betterworks.com/saml2/acs/`</span></span>

4. <span data-ttu-id="3bc80-161">Na seção **Domínio e URLs do BetterWorks**, se desejar configurar o aplicativo no **modo iniciado pelo SP**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="3bc80-161">On the **BetterWorks Domain and URLs** section, If you wish to configure the application in **SP initiated mode**, perform the following steps:</span></span>
    
    ![Configurar Logon Único](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_url1.png)

    <span data-ttu-id="3bc80-163">a.</span><span class="sxs-lookup"><span data-stu-id="3bc80-163">a.</span></span> <span data-ttu-id="3bc80-164">Clique em **Mostrar configurações de URL avançadas**.</span><span class="sxs-lookup"><span data-stu-id="3bc80-164">Click on the **Show advanced URL settings**.</span></span>

    <span data-ttu-id="3bc80-165">b.</span><span class="sxs-lookup"><span data-stu-id="3bc80-165">b.</span></span> <span data-ttu-id="3bc80-166">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://app.betterworks.com`</span><span class="sxs-lookup"><span data-stu-id="3bc80-166">In the **Sign On URL** textbox, type a URL using the following pattern: `https://app.betterworks.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3bc80-167">Esses não são valores reais.</span><span class="sxs-lookup"><span data-stu-id="3bc80-167">These are not real values.</span></span> <span data-ttu-id="3bc80-168">Atualize esses valores com a URL de Resposta, o Identificador e a URL de Logon real.</span><span class="sxs-lookup"><span data-stu-id="3bc80-168">Update these values with the Reply URL, Identifier and actual Sign On URL.</span></span> <span data-ttu-id="3bc80-169">Contate a [equipe de suporte do BetterWorks](mailto:support@betterworks.com) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="3bc80-169">Contact [BetterWorks support team](mailto:support@betterworks.com) to get these values.</span></span>
 
4. <span data-ttu-id="3bc80-170">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="3bc80-170">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_certificate.png)  

5. <span data-ttu-id="3bc80-172">O aplicativo BetterWorks espera que as declarações SAML estejam em um formato específico.</span><span class="sxs-lookup"><span data-stu-id="3bc80-172">BetterWorks application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="3bc80-173">Configure as declarações a seguir para este aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3bc80-173">Configure the following claims for this application.</span></span> <span data-ttu-id="3bc80-174">Gerencie os valores desses atributos na guia “**Atributo**” do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3bc80-174">You can manage the values of these attributes from the "**Attribute**" tab of the application.</span></span> <span data-ttu-id="3bc80-175">A captura de tela a seguir mostra um exemplo disso.</span><span class="sxs-lookup"><span data-stu-id="3bc80-175">The following screenshot shows an example for this.</span></span> 

    ![Configurar Logon Único](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_attribute.png)

6. <span data-ttu-id="3bc80-177">Na caixa de diálogo **Atributos de token SAML** , para cada linha mostrada na tabela a seguir, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="3bc80-177">On the **SAML token attributes** dialog, for each row shown in the table below, perform the following steps:</span></span>
 
   | <span data-ttu-id="3bc80-178">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="3bc80-178">Attribute Name</span></span> | <span data-ttu-id="3bc80-179">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="3bc80-179">Attribute Value</span></span> |
   | -------------- |  ------------ |
   | <span data-ttu-id="3bc80-180">saml_token</span><span class="sxs-lookup"><span data-stu-id="3bc80-180">saml_token</span></span>     | <span data-ttu-id="3bc80-181">bd189cf6-1701-11e6-8f90-d26992eca2a5</span><span class="sxs-lookup"><span data-stu-id="3bc80-181">bd189cf6-1701-11e6-8f90-d26992eca2a5</span></span> |

   <span data-ttu-id="3bc80-182">a.</span><span class="sxs-lookup"><span data-stu-id="3bc80-182">a.</span></span> <span data-ttu-id="3bc80-183">Clique em **Adicionar atributo** para abrir o diálogo **Adicionar Atributo**.</span><span class="sxs-lookup"><span data-stu-id="3bc80-183">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-betterworks-tutorial/tutorial_officespace_04.png)

    ![Configurar Logon Único](./media/active-directory-saas-betterworks-tutorial/tutorial_officespace_05.png)

   <span data-ttu-id="3bc80-186">b.</span><span class="sxs-lookup"><span data-stu-id="3bc80-186">b.</span></span> <span data-ttu-id="3bc80-187">Na caixa de texto **Nome** , digite o nome do atributo mostrado para essa linha.</span><span class="sxs-lookup"><span data-stu-id="3bc80-187">In the **Name** textbox, type the attribute name shown for that row.</span></span> 

   <span data-ttu-id="3bc80-188">c.</span><span class="sxs-lookup"><span data-stu-id="3bc80-188">c.</span></span> <span data-ttu-id="3bc80-189">Na lista **Valor**, digite o valor do atributo mostrado para essa linha.</span><span class="sxs-lookup"><span data-stu-id="3bc80-189">From the **Value** list, type the attribute value shown for that row.</span></span>
    
   <span data-ttu-id="3bc80-190">d.</span><span class="sxs-lookup"><span data-stu-id="3bc80-190">d.</span></span> <span data-ttu-id="3bc80-191">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="3bc80-191">Click **Ok**.</span></span>

7. <span data-ttu-id="3bc80-192">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="3bc80-192">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-betterworks-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="3bc80-194">Para configurar o logon único no lado do **BetterWorks**, é necessário enviar o **XML de Metadados** baixado para a [equipe de suporte do BetterWorks](mailto:support@betterworks.com).</span><span class="sxs-lookup"><span data-stu-id="3bc80-194">To configure single sign-on on **BetterWorks** side, you need to send the downloaded **Metadata XML** to [BetterWorks support team](mailto:support@betterworks.com).</span></span>


> [!TIP]
> <span data-ttu-id="3bc80-195">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="3bc80-195">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="3bc80-196">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="3bc80-196">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="3bc80-197">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3bc80-197">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3bc80-198">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3bc80-198">Creating an Azure AD test user</span></span>
<span data-ttu-id="3bc80-199">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="3bc80-199">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="3bc80-201">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="3bc80-201">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3bc80-202">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3bc80-202">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-betterworks-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3bc80-204">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="3bc80-204">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-betterworks-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3bc80-206">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3bc80-206">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-betterworks-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3bc80-208">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="3bc80-208">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-betterworks-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3bc80-210">a.</span><span class="sxs-lookup"><span data-stu-id="3bc80-210">a.</span></span> <span data-ttu-id="3bc80-211">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="3bc80-211">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3bc80-212">b.</span><span class="sxs-lookup"><span data-stu-id="3bc80-212">b.</span></span> <span data-ttu-id="3bc80-213">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="3bc80-213">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3bc80-214">c.</span><span class="sxs-lookup"><span data-stu-id="3bc80-214">c.</span></span> <span data-ttu-id="3bc80-215">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="3bc80-215">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="3bc80-216">d.</span><span class="sxs-lookup"><span data-stu-id="3bc80-216">d.</span></span> <span data-ttu-id="3bc80-217">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="3bc80-217">Click **Create**.</span></span>
 
### <a name="creating-a-betterworks-test-user"></a><span data-ttu-id="3bc80-218">Criando um usuário de teste do BetterWorks</span><span class="sxs-lookup"><span data-stu-id="3bc80-218">Creating a BetterWorks test user</span></span>

<span data-ttu-id="3bc80-219">Nesta seção, você criará um usuário chamado Brenda Fernandes no BetterWorks.</span><span class="sxs-lookup"><span data-stu-id="3bc80-219">In this section, you create a user called Britta Simon in BetterWorks.</span></span> <span data-ttu-id="3bc80-220">Trabalhe com a [equipe de suporte do BetterWorks](mailto:support@betterworks.com) para adicionar os usuários à plataforma BetterWorks.</span><span class="sxs-lookup"><span data-stu-id="3bc80-220">Work with [BetterWorks support team](mailto:support@betterworks.com) to add the users in the BetterWorks platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="3bc80-221">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3bc80-221">Assigning the Azure AD test user</span></span>

<span data-ttu-id="3bc80-222">Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo acesso ao BetterWorks.</span><span class="sxs-lookup"><span data-stu-id="3bc80-222">In this section, you enable Britta Simon to use Azure single sign-on by granting access to BetterWorks.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="3bc80-224">**Para atribuir Brenda Fernandes ao BetterWorks, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="3bc80-224">**To assign Britta Simon to BetterWorks, perform the following steps:**</span></span>

1. <span data-ttu-id="3bc80-225">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="3bc80-225">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="3bc80-227">Na lista de aplicativos, escolha **BetterWorks**.</span><span class="sxs-lookup"><span data-stu-id="3bc80-227">In the applications list, select **BetterWorks**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_app.png) 

3. <span data-ttu-id="3bc80-229">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="3bc80-229">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="3bc80-231">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="3bc80-231">Click **Add** button.</span></span> <span data-ttu-id="3bc80-232">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3bc80-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="3bc80-234">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="3bc80-234">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="3bc80-235">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3bc80-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3bc80-236">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3bc80-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3bc80-237">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="3bc80-237">Testing single sign-on</span></span>

<span data-ttu-id="3bc80-238">O objetivo desta seção é testar sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="3bc80-238">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="3bc80-239">Ao clicar no bloco BetterWorks no Painel de Acesso, você fará logon automaticamente no seu aplicativo BetterWorks.</span><span class="sxs-lookup"><span data-stu-id="3bc80-239">When you click the BetterWorks tile in the Access Panel, you should get automatically signed-on to your BetterWorks application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3bc80-240">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="3bc80-240">Additional resources</span></span>

* [<span data-ttu-id="3bc80-241">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="3bc80-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3bc80-242">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3bc80-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_203.png

