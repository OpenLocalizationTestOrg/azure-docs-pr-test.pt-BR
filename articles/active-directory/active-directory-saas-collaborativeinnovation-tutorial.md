---
title: "Tutorial: Integração do Azure Active Directory com Inovação Colaborativa | Microsoft Docs"
description: "Saiba como configurar logon único entre o Azure Active Directory e a Inovação Colaborativa."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bba95df3-75a4-4a93-8805-b3a8aa3d4861
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: jeedes
ms.openlocfilehash: 5706ba9f4e7c92de77a0edc5146aa150de379c9f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-collaborative-innovation"></a><span data-ttu-id="47e4c-103">Tutorial: Integração do Azure Active Directory com Inovação Colaborativa</span><span class="sxs-lookup"><span data-stu-id="47e4c-103">Tutorial: Azure Active Directory integration with Collaborative Innovation</span></span>

<span data-ttu-id="47e4c-104">Neste tutorial, você aprenderá a integrar Inovação Colaborativa ao Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="47e4c-104">In this tutorial, you learn how to integrate Collaborative Innovation with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="47e4c-105">Integrar Inovação Colaborativa ao Azure AD oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="47e4c-105">Integrating Collaborative Innovation with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="47e4c-106">Você pode controlar no Azure AD quem tem acesso à Inovação Colaborativa</span><span class="sxs-lookup"><span data-stu-id="47e4c-106">You can control in Azure AD who has access to Collaborative Innovation</span></span>
- <span data-ttu-id="47e4c-107">Você pode habilitar seus usuários logon automático na Inovação Colaborativa (Logon Único) com suas respectivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="47e4c-107">You can enable your users to automatically get signed-on to Collaborative Innovation (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="47e4c-108">Você pode gerenciar suas contas em um única localização: o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="47e4c-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="47e4c-109">Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="47e4c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="47e4c-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="47e4c-110">Prerequisites</span></span>

<span data-ttu-id="47e4c-111">Para configurar a integração do Azure AD à Inovação Colaborativa, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="47e4c-111">To configure Azure AD integration with Collaborative Innovation, you need the following items:</span></span>

- <span data-ttu-id="47e4c-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="47e4c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="47e4c-113">Um logon único da Inovação Colaborativa em uma assinatura habilitada</span><span class="sxs-lookup"><span data-stu-id="47e4c-113">A Collaborative Innovation single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="47e4c-114">Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="47e4c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="47e4c-115">Para testar as etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="47e4c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="47e4c-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="47e4c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="47e4c-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="47e4c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="47e4c-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="47e4c-118">Scenario description</span></span>
<span data-ttu-id="47e4c-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="47e4c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="47e4c-120">O cenário descrito neste tutorial consiste em dois blocos de construção principais:</span><span class="sxs-lookup"><span data-stu-id="47e4c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="47e4c-121">Adicionando Inovação Colaborativa da galeria</span><span class="sxs-lookup"><span data-stu-id="47e4c-121">Adding Collaborative Innovation from the gallery</span></span>
2. <span data-ttu-id="47e4c-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="47e4c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-collaborative-innovation-from-the-gallery"></a><span data-ttu-id="47e4c-123">Adicionando Inovação Colaborativa da galeria</span><span class="sxs-lookup"><span data-stu-id="47e4c-123">Adding Collaborative Innovation from the gallery</span></span>
<span data-ttu-id="47e4c-124">Para configurar a integração de Inovação Colaborativa ao Azure AD, você precisa adicionar a Inovação Colaborativa da galeria à sua lista de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="47e4c-124">To configure the integration of Collaborative Innovation into Azure AD, you need to add Collaborative Innovation from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="47e4c-125">**Para adicionar a Inovação Colaborativa da galeria, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="47e4c-125">**To add Collaborative Innovation from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="47e4c-126">No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="47e4c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="47e4c-128">Navegue até **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="47e4c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="47e4c-129">Em seguida, vá para **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="47e4c-129">Then go to **All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="47e4c-131">Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="47e4c-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="47e4c-133">Na caixa de pesquisa, digite **Inovação Colaborativa**.</span><span class="sxs-lookup"><span data-stu-id="47e4c-133">In the search box, type **Collaborative Innovation**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_search.png)

5. <span data-ttu-id="47e4c-135">No painel de resultados, selecione **Inovação Colaborativa** e, em seguida, clique no botão **Adicionar** para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="47e4c-135">In the results panel, select **Collaborative Innovation**, and then click **Add** button to add the application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="47e4c-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="47e4c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="47e4c-138">Nesta seção, você configurará e testará o logon único do Azure AD com a Inovação Colaborativa com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="47e4c-138">In this section, you configure and test Azure AD single sign-on with Collaborative Innovation based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="47e4c-139">Para que o logon único funcione, o Azure AD precisa saber qual usuário equivalente na Inovação Colaborativa é um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="47e4c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Collaborative Innovation is to a user in Azure AD.</span></span> <span data-ttu-id="47e4c-140">Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado da Inovação Colaborativa.</span><span class="sxs-lookup"><span data-stu-id="47e4c-140">In other words, a link relationship between an Azure AD user and the related user in Collaborative Innovation needs to be established.</span></span>

<span data-ttu-id="47e4c-141">Na Inovação Colaborativa, atribua o valor de **nome de usuário** no Azure AD como o valor de **Nome de usuário** para estabelecer a relação de vínculo.</span><span class="sxs-lookup"><span data-stu-id="47e4c-141">In Collaborative Innovation, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="47e4c-142">Para configurar e testar o logon único do Azure AD com a Inovação Colaborativa, você precisa concluir os seguintes blocos de construção:</span><span class="sxs-lookup"><span data-stu-id="47e4c-142">To configure and test Azure AD single sign-on with Collaborative Innovation, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="47e4c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="47e4c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="47e4c-144">**[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** : para testar o logon único do AD do Azure com Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="47e4c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="47e4c-145">**[Criar um usuário de teste da Inovação Colaborativa](#creating-a-collaborative-innovation-test-user)** – ter um equivalente de Brenda Fernandes na Inovação Colaborativa que esteja vinculado à representação do Azure AD do usuário.</span><span class="sxs-lookup"><span data-stu-id="47e4c-145">**[Creating a Collaborative Innovation test user](#creating-a-collaborative-innovation-test-user)** - to have a counterpart of Britta Simon in Collaborative Innovation that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="47e4c-146">**[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** : para permitir que Brenda Fernandes use o logon único do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="47e4c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="47e4c-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para verificar se a configuração funciona.</span><span class="sxs-lookup"><span data-stu-id="47e4c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="47e4c-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="47e4c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="47e4c-149">Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único em seu aplicativo Inovação Colaborativa.</span><span class="sxs-lookup"><span data-stu-id="47e4c-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Collaborative Innovation application.</span></span>

<span data-ttu-id="47e4c-150">**Para configurar o logon único do Azure AD com inovação colaborativa, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="47e4c-150">**To configure Azure AD single sign-on with Collaborative Innovation, perform the following steps:**</span></span>

1. <span data-ttu-id="47e4c-151">No portal do Azure, na página de integração de aplicativos **Inovação Colaborativa**, clique em **Logon Único**.</span><span class="sxs-lookup"><span data-stu-id="47e4c-151">In the Azure portal, on the **Collaborative Innovation** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="47e4c-153">Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.</span><span class="sxs-lookup"><span data-stu-id="47e4c-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_samlbase.png)

3. <span data-ttu-id="47e4c-155">Na seção **Domínio da Inovação Colaborativa e URLs**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="47e4c-155">On the **Collaborative Innovation Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_url.png)

    <span data-ttu-id="47e4c-157">a.</span><span class="sxs-lookup"><span data-stu-id="47e4c-157">a.</span></span> <span data-ttu-id="47e4c-158">Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<instancename>.foundry.<companyname>.com/`</span><span class="sxs-lookup"><span data-stu-id="47e4c-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<instancename>.foundry.<companyname>.com/`</span></span>

    <span data-ttu-id="47e4c-159">b.</span><span class="sxs-lookup"><span data-stu-id="47e4c-159">b.</span></span> <span data-ttu-id="47e4c-160">Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<instancename>.foundry.<companyname>.com`</span><span class="sxs-lookup"><span data-stu-id="47e4c-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<instancename>.foundry.<companyname>.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="47e4c-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="47e4c-161">These values are not real.</span></span> <span data-ttu-id="47e4c-162">Atualize esses valores com a URL de Entrada e o Identificador reais.</span><span class="sxs-lookup"><span data-stu-id="47e4c-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="47e4c-163">Entre em contato com a [equipe de suporte do Cliente de Inovação Colaborativa](https://www.unilever.com/contact/) para obter esses valores.</span><span class="sxs-lookup"><span data-stu-id="47e4c-163">Contact [Collaborative Innovation Client support team](https://www.unilever.com/contact/) to get these values.</span></span>  

4. <span data-ttu-id="47e4c-164">O aplicativo de Inovação Colaborativa espera as asserções SAML em um formato específico.</span><span class="sxs-lookup"><span data-stu-id="47e4c-164">Collaborative Innovation application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="47e4c-165">Configure as seguintes declarações para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="47e4c-165">Please configure the following claims for this application.</span></span> <span data-ttu-id="47e4c-166">Você pode gerenciar os valores desses atributos da seção "**Atributos de Usuário**" na página de integração do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="47e4c-166">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="47e4c-167">A captura de tela a seguir mostra um exemplo disso.</span><span class="sxs-lookup"><span data-stu-id="47e4c-167">The following screenshot shows an example for this.</span></span>
    
    ![Configurar Logon Único](./media/active-directory-saas-collaborativeinnovation-tutorial/attribute.png)
    
5. <span data-ttu-id="47e4c-169">Clique na caixa de seleção **Exibir e editar todos os outros atributos de usuário** na seção **Atributos de Usuário** para expandir os atributos.</span><span class="sxs-lookup"><span data-stu-id="47e4c-169">Click **View and edit all other user attributes** checkbox in the **User Attributes** section to expand the attributes.</span></span> <span data-ttu-id="47e4c-170">Realize as seguintes etapas em cada um dos atributos exibidos:</span><span class="sxs-lookup"><span data-stu-id="47e4c-170">Perform the following steps on each of the displayed attributes-</span></span>

    | <span data-ttu-id="47e4c-171">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="47e4c-171">Attribute Name</span></span> | <span data-ttu-id="47e4c-172">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="47e4c-172">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="47e4c-173">givenname</span><span class="sxs-lookup"><span data-stu-id="47e4c-173">givenname</span></span> | <span data-ttu-id="47e4c-174">user.givenname</span><span class="sxs-lookup"><span data-stu-id="47e4c-174">user.givenname</span></span> |
    | <span data-ttu-id="47e4c-175">sobrenome</span><span class="sxs-lookup"><span data-stu-id="47e4c-175">surname</span></span> | <span data-ttu-id="47e4c-176">user.surname</span><span class="sxs-lookup"><span data-stu-id="47e4c-176">user.surname</span></span> |
    | <span data-ttu-id="47e4c-177">emailaddress</span><span class="sxs-lookup"><span data-stu-id="47e4c-177">emailaddress</span></span> | <span data-ttu-id="47e4c-178">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="47e4c-178">user.userprincipalname</span></span> |
    | <span data-ttu-id="47e4c-179">name</span><span class="sxs-lookup"><span data-stu-id="47e4c-179">name</span></span> | <span data-ttu-id="47e4c-180">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="47e4c-180">user.userprincipalname</span></span> |

    <span data-ttu-id="47e4c-181">a.</span><span class="sxs-lookup"><span data-stu-id="47e4c-181">a.</span></span> <span data-ttu-id="47e4c-182">Clique no atributo para abrir a janela **Editar Atributo**.</span><span class="sxs-lookup"><span data-stu-id="47e4c-182">Click the attribute to open the **Edit Attribute** window.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-collaborativeinnovation-tutorial/url_update.png)

    <span data-ttu-id="47e4c-184">b.</span><span class="sxs-lookup"><span data-stu-id="47e4c-184">b.</span></span> <span data-ttu-id="47e4c-185">Exclua o valor da URL do **Namespace**.</span><span class="sxs-lookup"><span data-stu-id="47e4c-185">Delete the URL value from the **Namespace**.</span></span>
    
    <span data-ttu-id="47e4c-186">c.</span><span class="sxs-lookup"><span data-stu-id="47e4c-186">c.</span></span> <span data-ttu-id="47e4c-187">Clique em **OK** para salvar a configuração.</span><span class="sxs-lookup"><span data-stu-id="47e4c-187">Click **Ok** to save the setting.</span></span>

6. <span data-ttu-id="47e4c-188">Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.</span><span class="sxs-lookup"><span data-stu-id="47e4c-188">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar o logon único](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_certificate.png) 

7. <span data-ttu-id="47e4c-190">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="47e4c-190">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="47e4c-192">Para configurar o logon único o lado de **Inovação Colaborativa**, você precisa enviar o **XML de Metadados** baixado para a [equipe de suporte da Inovação Colaborativa](https://www.unilever.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="47e4c-192">To configure single sign-on on **Collaborative Innovation** side, you need to send the downloaded **Metadata XML** to [Collaborative Innovation support team](https://www.unilever.com/contact/).</span></span> <span data-ttu-id="47e4c-193">Eles definem essa configuração para ter a conexão de SSO do SAML definida corretamente em ambos os lados.</span><span class="sxs-lookup"><span data-stu-id="47e4c-193">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="47e4c-194">É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="47e4c-194">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="47e4c-195">Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="47e4c-195">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="47e4c-196">Saiba mais sobre a funcionalidade de documentação inserida aqui: [Documentação inserida do Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="47e4c-196">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="47e4c-197">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="47e4c-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="47e4c-198">O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="47e4c-198">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="47e4c-200">**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="47e4c-200">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="47e4c-201">No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="47e4c-201">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-collaborativeinnovation-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="47e4c-203">Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="47e4c-203">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-collaborativeinnovation-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="47e4c-205">Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="47e4c-205">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-collaborativeinnovation-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="47e4c-207">Na página do diálogo **Usuário**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="47e4c-207">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-collaborativeinnovation-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="47e4c-209">a.</span><span class="sxs-lookup"><span data-stu-id="47e4c-209">a.</span></span> <span data-ttu-id="47e4c-210">Na caixa de texto **Nome**, digite **Brenda Fernandes**.</span><span class="sxs-lookup"><span data-stu-id="47e4c-210">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="47e4c-211">b.</span><span class="sxs-lookup"><span data-stu-id="47e4c-211">b.</span></span> <span data-ttu-id="47e4c-212">Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.</span><span class="sxs-lookup"><span data-stu-id="47e4c-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="47e4c-213">c.</span><span class="sxs-lookup"><span data-stu-id="47e4c-213">c.</span></span> <span data-ttu-id="47e4c-214">Selecione **Mostrar senha** e anote o valor de **senha**.</span><span class="sxs-lookup"><span data-stu-id="47e4c-214">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="47e4c-215">d.</span><span class="sxs-lookup"><span data-stu-id="47e4c-215">d.</span></span> <span data-ttu-id="47e4c-216">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="47e4c-216">Click **Create**.</span></span>
 
### <a name="creating-a-collaborative-innovation-test-user"></a><span data-ttu-id="47e4c-217">Como criar um usuário de teste da Inovação Colaborativa</span><span class="sxs-lookup"><span data-stu-id="47e4c-217">Creating a Collaborative Innovation test user</span></span>

<span data-ttu-id="47e4c-218">Para permitir que os usuários do Azure AD façam logon na Inovação Colaborativa, eles devem ser provisionados na Inovação Colaborativa.</span><span class="sxs-lookup"><span data-stu-id="47e4c-218">To enable Azure AD users to log in to Collaborative Innovation, they must be provisioned into Collaborative Innovation.</span></span>  

<span data-ttu-id="47e4c-219">No caso deste aplicativo, o provisionamento é automático, uma vez que o aplicativo dá suporte a provisionamento do usuário just-in-time.</span><span class="sxs-lookup"><span data-stu-id="47e4c-219">In case of this application provisioning is automatic as the application supports just in time user provisioning.</span></span> <span data-ttu-id="47e4c-220">Assim, não é necessário executar nenhuma etapa aqui.</span><span class="sxs-lookup"><span data-stu-id="47e4c-220">So there is no need to perform any steps here.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="47e4c-221">Atribuição do usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="47e4c-221">Assigning the Azure AD test user</span></span>

<span data-ttu-id="47e4c-222">Nesta seção, você habilitará Brenda Fernandes a usar o logon único do Azure concedendo acesso à Inovação Colaborativa.</span><span class="sxs-lookup"><span data-stu-id="47e4c-222">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Collaborative Innovation.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="47e4c-224">**Para atribuir Brenda Fernandes à Inovação Colaborativa, execute as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="47e4c-224">**To assign Britta Simon to Collaborative Innovation, perform the following steps:**</span></span>

1. <span data-ttu-id="47e4c-225">No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="47e4c-225">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="47e4c-227">Na lista de aplicativos, selecione **Inovação Colaborativa**.</span><span class="sxs-lookup"><span data-stu-id="47e4c-227">In the applications list, select **Collaborative Innovation**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_app.png) 

3. <span data-ttu-id="47e4c-229">No menu à esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="47e4c-229">In the menu on the left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="47e4c-231">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="47e4c-231">Click **Add** button.</span></span> <span data-ttu-id="47e4c-232">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="47e4c-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="47e4c-234">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="47e4c-234">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="47e4c-235">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="47e4c-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="47e4c-236">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="47e4c-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="47e4c-237">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="47e4c-237">Testing single sign-on</span></span>

<span data-ttu-id="47e4c-238">Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.</span><span class="sxs-lookup"><span data-stu-id="47e4c-238">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="47e4c-239">Quando você clicar no bloco de Inovação Colaborativa no Painel de Acesso, deve obter a página de logon do aplicativo Inovação Colaborativa.</span><span class="sxs-lookup"><span data-stu-id="47e4c-239">When you click the Collaborative Innovation tile in the Access Panel, you should get login page of Collaborative Innovation application.</span></span>
<span data-ttu-id="47e4c-240">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="47e4c-240">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="47e4c-241">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="47e4c-241">Additional resources</span></span>

* [<span data-ttu-id="47e4c-242">Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="47e4c-242">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="47e4c-243">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="47e4c-243">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_203.png

